---
layout: post
title: "Learning a New Language"
permalink: learning-a-new-language
date: 2016-08-16 22:06:53
comments: true
description: "Learning a New Language"
tags:
- elixir
- erlang
- functional
- language
---

Every now and then I get an itch. An itch to learn something new, to fully immerse myself in a new language, framework, or library. I've had this itch for a while now, but for a number of reasons haven't been able to scratch it. Well, it finally became unbearable and I've now started learning [Elixir](http://elixir-lang.org/)–a functional language that runs on the Erlang VM.

Why Elixir? When I first started looking into a new language, I focused on Go and Rust. Both look like amazing languages, and Go in particular has a vibrant community around it. However, I couldn't choose between them primarily because neither of the two languages felt all that exotic or sexy. Yes. Sexy. I then came across Elixir, and it was the perfect language to get my feet wet with a pure functional language.

At first I still completely wasn't sold, so I started reading through the docs until I came across some patterns and capabilities of the language. Firstly, its a functional language, where _all_ data is immutable, even primatives. Which, from my JavaScript background, is highly appealing. Secondly, Elixir's pattern matching is very elegant and deeply rooted in the language and its idioms. Lastly, and arguably most importantly, being built on the Erlang VM, the language utilizes processes to achieve excellent fault-tolerance. And when I say processes, I do not mean at the OS level; These are Erlang processes, which are scheduled by the Erlang VM and do not share state or memory with other running processes. Additionaly, processes can be easily distributed, even across machines–making distributed systems easier to manage.

I am still only a few days in to learning this fantastic language, but I expect it will be a real challenge and joy to work with. While the community surrounding Elixir is still young and small, I see that it will continue to grow and gain traction as the industry continues to move towards more distributed architectures.
