---
layout: post
title: "Programmatic Promise Chaining"
permalink: programmatic-promise-chaining
comments: true
date: "2016-08-15"
tags:
- javascript
- promises
- es6
---

If you've used JavaScript Promises, then you've probably used `Promise.all()` as well. If not, `Promise.all()` returns a Promise and resolves once all individual Promises have resolved. It is important to note, howevever, that each Promises is executed _concurrently_. Generally speaking, this is a good thing as it reduced bottlenecks. However, this also opens your application up to issues with race conditions.

This is usually a fairly easy issue to resolve. An instance of Promise will expose the method, `then()`, which allows you to control the flow of Promises. The problem comes when you need the brevity of `Promises.all()` and the flow of a `.then()` Promise chain. Also, what if the number and/or composition of Promises isn't known until runtime? Clearly there is a need for a synchronous version of `Promise.all()`. By synchronous I mean each Promise runs in sequence, but the overall process would still happen outside the main application thread.

Luckily, there is a way to handle such situations. As an example, we'll create a simple middleware handler class.

{% highlight javascript %}
class MiddlewareHandler {
    constructor() {
        this.middleware = []
    }

    // Add a new middleware function
    use(fn) {
        this.middleware.push(fn)
        return this
    }

    // Execute the middleware
    run(...args) {
        return this._getPromiseSequence(this.middleware, args)
    }

    // Get a Promise sequence
    _getPromiseSequence(promises, args) {
        return promises.reduce((chain, fn) => {
            return chain.then(result => { return fn.apply(fn, result) })
        }, Promise.resolve(args))
    }
}

// New handler instance
const handler = new MiddlewareHandler()

// Add middleware to increment response count
handler.use((req, res) => {
    return [
        req,
        Object.assign({}, res, { count: ++res.count })
    ]
})

// Add middleware to increment response count after a 200ms delay
handler.use((req, res) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve([
                req,
                Object.assign({}, res, { count: ++res.count })
            ])
        }, 200)
    })
})

// Add middleware to update the response status
handler.use((req, res) => {
    return [
        req,
        Object.assign({}, res, { status: 403 })
    ]
})

// Run the middleware
handler
    .run({ from: 'someone' }, { count: 0, status: 200 })
    .then(([req, res]) => { console.log(res) })
{% endhighlight %}

If you run the above example, you should see the following in the console:

{% highlight javascript %}
{ count: 2, status: 403 }
{% endhighlight %}

In this example, we define a new class, `MiddlewareHandler`, which is responsible for all logic surrounding middleware. The `use()` method allows us to push a new middleware function into the queue, and `run()` will execute each of the middleware functions and return a Promise. In order to maintain some level of immutability, the return value (or resolved value) of one function is the input of the next.

The private method, `_getPromiseSequence()` is what constructs the Promise chain from the array of middleware functions. It works by using `Array.reduce()` to iterate though each of the functions.

There are two important things to note in this pattern. First, in order to pass multiple arguments to each middleware function, the functions must return or resolve an array, where each element corresponds to one of the arguments. This array is then passed to `apply()` in the `_getPromiseSequence()` method so that each element can be passed an individual arguments. Secondly, because of the nature of `then()`, a middleware function does not have to return a Promise; Any `return` value is treated as a `Promise.resolve()` internally. Similarly, any `throw` is treated as `Promise.reject()`.

This is an extremely useful pattern and has many applications, but it should be used only when necessary.
