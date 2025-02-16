---
layout: post
title: "How to get started with web development in 2025?"
date: 2025-02-16 09:02:05
description: The Evolution of Web Development and Where to Begin in 2025
tags: [web development, web frameworks]
---

## The Evolution of Web Development and Where to Begin in 2025

In recent years, technologies like ChatGPT have revolutionized the way we work, making web application development more accessible than ever. However, while creating web applications has become easier, it still comes with unique challenges. The web wasn’t originally designed as an application platform—it was built for sharing documents. This means web developers must navigate constraints like limited bandwidth and performance optimization to deliver efficient and scalable applications.

In this post, I’ll explore how we got to where we are today in web development and provide some guidance on how to get started in 2025. This post was inspired by a question I received after a recent lecture (see slides↗), and it’s tailored for beginners looking to step into the world of web development.

## How Did We Arrive at Modern Web Applications?

The web has become the go-to platform for applications due to its universal accessibility. However, it wasn’t initially built for complex applications. The shift started in the late 1990s with AJAX, allowing websites to fetch data from the server without requiring a full page reload. This innovation paved the way for Single-Page Applications (SPAs), which remain a dominant model for building interactive web applications.

Despite their advantages, SPAs introduce some challenges. They often require downloading large JavaScript bundles, increasing load times and impacting performance. While techniques like code-splitting help, they only mitigate the problem rather than eliminate it. According to the Web Almanac↗, the median page size on mobile devices grew nearly sixfold between 2012 and 2022, contributing significantly to global web traffic (DataReportal↗). Heavy use of JavaScript, third-party scripts, and oversized images are major culprits, leading developers to explore ways to make web applications leaner and more efficient.

Newer frameworks are tackling this issue with innovative approaches. For example, Astro↗ introduces an "islands architecture" to load only the necessary JavaScript, while Qwik↗ leverages "resumability" (see paper Resumability — A New Primitive for Developing Web Applications↗) to optimize performance. Similarly, React Server Components↗ aim to reduce client-side rendering overhead by shifting some logic to the server.

## The Role of Web Frameworks

Web frameworks serve several purposes:

- Solve common challenges in web development.
- Capture the technical philosophy of their creators.
- Reduce redundancy across projects.
- Speed up development.

However, frameworks aren’t always a perfect fit. Strongly opinionated frameworks may force you into patterns that don’t suit your project, leading to workarounds or unnecessary complexity. While some believe web frameworks are innovating at a slower pace, there are still exciting developments. Solid.js↗ pushes reactivity boundaries, Marko.js↗ reimagines templating, and emerging experimental approaches (such as merging HTML with LISP↗) continue to expand possibilities.

Frameworks also help fill gaps left by the web platform, which was never originally intended for app development. While web standards continue evolving, user expectations for web applications are constantly rising. As a result, developers often turn to frameworks to bridge the gap between what browsers natively support and what modern apps demand.

Regardless of which framework you choose, most share common architectural concepts:

1. Component-Based Architecture – Web apps are built using reusable components containing markup, logic, and state.

2. Templating – A system that connects application state to the user interface.

3. Hydration – A technique where static server-rendered pages become interactive on the client side. Qwik’s "resumability" model aims to replace hydration with a more efficient alternative.

## Can You Build a Web App Without a Framework?

It’s a valid question: do we still need frameworks to build web applications? The answer is, as always, "it depends." There are many things you can achieve using just the web platform, and some movements, like "HTML First development↗," advocate minimizing reliance on JavaScript. You’d be surprised how much can be accomplished with well-structured HTML and CSS alone, with JavaScript only added when necessary.

This doesn’t mean avoiding frameworks entirely, but rather embracing native web technologies more, making your code more portable across different tools. Web Components↗, for instance, offer a standardized approach to encapsulated components that work without framework dependencies.

## Invest in the Fundamentals

If you want long-term success in web development, prioritize learning the fundamentals. Technologies like HTML, CSS, JavaScript, and the DOM evolve slowly, making them valuable skills that persist over time. While frameworks change, understanding core concepts will help you adapt more easily.

At the same time, when learning frameworks, focus on grasping overarching principles rather than memorizing syntax. The ability to transfer knowledge across frameworks is a huge asset, especially in an industry where tools frequently evolve.

## Use AI Tools to Enhance Learning

AI-powered tools can accelerate your learning process by summarizing documentation, converting sketches to HTML, and generating code snippets. While these tools aren’t perfect, they can be useful aids in your workflow. However, always verify the information they provide, and document your prompts to refine your interactions with AI.

## Conclusion

2025 is an exciting time to get into web development. The landscape is evolving, particularly with the increasing influence of AI on workflows and development practices. If you’re just starting out, begin with a project that excites you, then explore the technologies required to bring it to life. Your vision will naturally evolve as your skills grow, which is a normal part of the learning process.

Above all, focus on understanding the foundations of web development. Mastering HTML, CSS, JavaScript, and the DOM will serve you well regardless of which frameworks come and go. While frameworks are valuable, they’re most effective when used in conjunction with a strong understanding of the core web technologies they build upon.
