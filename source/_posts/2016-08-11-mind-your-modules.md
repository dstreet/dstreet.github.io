---
layout: post
title: "Mind Your Modules"
permalink: mind-your-modules
date: 2016-08-11 16:04:55
comments: true
tags:
- JavaScript
- es6
- CommonJS
- modules
- performance
---

Modern JavaScript development makes extensive use of modules both on the client side as well as the server side. Let me just say, modules are fantastic! They allow us to write cleaner, and more reusable code and are an integral part of Node.js development as well as most newer frontend frameworks. The newest JavaScript spec, es6 (ES2015), has even provided new language constructs for utilizing modules: `import` and `export`.

When it comes to modules there are three main camps, CommonJS, es6 modules, and AMD. The last of which has fallen out of grace over the past few years, so I won't touch on that anymore than I already have.

CommonJS is common in Node.js development and is the primary means for including modules when using bundlers such as Browserify or Webpack:

{% highlight javascript %}
// module.js or module/index.js
module.exports = { foo: 'foo' }

// module2.js
exports.foo = 'foo'
exports.bar = 'bar'

// main.js
const myModule = require('./module')
const foo      = require('./module2').foo
{% endhighlight %}

The CommonJS implementation above written for es6 modules would look something like:

{% highlight javascript %}
// module.js or module/index.js
export default { foo: 'foo' }

// module2.js
export const foo = 'foo'
export const bar = 'bar'

// main.js
import myModule from './module'
import { foo } from './module2'
{% endhighlight %}

For both examples, I want to call special attention to module2.js, as they export multiple properties. Whereas module.js exports only a single "default" property.

At the time of writing this, the es6 language features for modules is not widely supported by browsers or even Node.js; As such, a transpiler and bundler is needed in order to use these. This is typically a combination of Babel with either Browserify or Webpack.

To over simplify the way these bundlers work, they append the contents of these files being imported to a final "bundled" file. To no fault of the bundlers, this can lead to some optimization concerns, especially when importing a file that contains multiple exports. Because the final bundle contains the entire file contents of an imported module, there is the potential to include a large amount of unused code. This is particularly concerning for frontend applications where file size and the time it takes for browsers to parse JavaScript are extremely important for performance reasons.

To avoid this issue, it is best to avoid modules that have multiple exports unless it is absolutely necessary or you know that you will be utilizing each of the exports. In order to achieve this, each module can be broken out into its own file. If we were to re-architect our original example, it might look something like:

{% highlight javascript %}
// module.js or module/index.js
module.exports = { foo: 'foo' }

// module2/foo.js
module.exports = 'foo'

// module2/bar.js
module.exports = 'bar'

// main.js
const myModule = require('module')
const foo      = require('module2/foo')
{% endhighlight %}

and in es6:

{% highlight javascript %}
// module.js or module/index.js
export default { foo: 'foo' }

// module2/foo.js
export default 'foo'

// module2/bar.js
export default 'bar'

// main.js
import myModule from './module'
import foo from './module2/foo'
{% endhighlight %}

From the perspective of main.js, the result is the same. It has access to all the modules it needs. The only difference being, that the resulting bundle file does not include `bar`, the module not explicitly imported in main.js.

This pattern is especially important for large libraries or set of utilities. The utility library, lodash, for instance, has already adopted this pattern knowing that most users will only use a handful of the methods it provides.
