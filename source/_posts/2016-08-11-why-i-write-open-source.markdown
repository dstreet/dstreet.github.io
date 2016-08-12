---
layout: post
title: "Why I Write Open Source"
permalink: why-write-open-source
comments: true
date: "2016-08-12"
tags:
- open source
- free software
- licensing
---

Whether you are an individual, organization, business, or government entity releasing, maintaining, and contributing to open source software has many benefits. There are numerous articles, like <a href="http://www.infoworld.com/article/3028600/open-source-tools/whats-the-real-reason-microsoft-and-google-are-releasing-open-source.html" target="_blank">this one from InfoWorld</a>, on the subject. In fact, I could spend a lot time talking about each of these individually. Instead, I'm going to focus on what drives _me_ to write and release open source software, and why I use the licenses I do.

Before I begin, its probably worth noting that I have slightly obsessive tendencies. That combined with a passion for all things programming lead to the _need_ to solve problems, especially those relating to programming and software development themselves. This, of course, leads to the development of tooling, libraries, and frameworks to solve these problems.

I think most people can agree this makes sense; I write sofware to solve the problems that I face. But why release it as open source? I could say that I release it under an open source license because its a great learning expercise, it benefits the larger development community, or just because I don't know what else to do with it. While these are all valid true, they are not my _primary_ motivation.

The truth is actually much more selfish. When I first release something into the wild on GitHub, I watch the traffic graphs obsessively. For me, there is nothing more exciting in development than having someone else use your work. I try not to be a star chaser, but there is a certain high when you get that first star. The first Pull Request is even more exciting; You've released something that people _actually_ like and find useful! Who doesn't like a little validation every now and then?

So, sure my reasons for realeasing open source software is mostly self-serving. The licenses I choose, however, are not. When choosing a license, I typically fall back to one of two licenses; The choice depends solely on how the work is intended to be used.

Libraries and frameworks are always released under [The MIT License](https://opensource.org/licenses/MIT). This allows the works to reach a larger audience, as it is an _extremely_ permissive license. I do much care how you use these works, as long as you use them! After all, the whole point of a library or framework is build something.

Occasionally I will create a piece of _software_–something that is not meant to be included in a codebase, but is rather tool. When releaseing a piece of work like this, I fallback to the [GNU General Public License, version 3](https://opensource.org/licenses/GPL-3.0). This is a _less_ permissive license, so why would I choose it? Since the final product is a piece of "software" and not a library used in the _making_ of sofware, I want it and any derivative works to remain _free_ (as in freedom), and the GPL ensures this. The free software landscape is vibrant and diverse, and I wish for it stay that way.

When it comes to deciding whether or not to release a project as open source its important to understand your motivations. In the case of open source, this helps form an idea of what your commitment might be and how much time you expect to invest in these projects. What are your motivations for writing open source, or conversely, choosing _not_ to release open source?

---

For those of you finely atuned to the nuances between "open source" and "free software", you may be asking why I speak more to "open source" than "free software," and do I fall more heavily on the "open source" side. To that, I would say "its complicated." In this article I have used both terms, and have done so with great intent. In a very general way, I write "open source" libraries and "free software" programs.

When I develop a piece of software, I don't want it to infringe on any user's freedoms. Nor do I want any derivative work to infringe on any user's freedoms.

For libraries, I fully accept that in order for my code to be used, it will at times need to be used in a closed source environment. However, this is not say that I condone using these libraries to create software that infringes upon a user's freedoms.

For more information on open source and free software, please check out the "official" definitions of [Open Source](https://opensource.org/osd) and [Free Software](https://www.gnu.org/philosophy/free-sw.html).
