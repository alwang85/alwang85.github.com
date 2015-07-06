---
layout: post
title: "Thoughts on book part 1: Node.js Design Patterns"
description: ""
category: 
tags: []
---

# Thoughts

tl;dr:  This is a wonderful book so far. In my quest to further my knowledge in the MEAN stack, I chose a book called "Node.js Design Patterns" by Mario Casciaro. I have many books that talks about JavaScript behavior, but this book ties design patterns to JavaScript and Node.js very well. What I felt for "JavaScript Patterns" did for me for Javascript, I feel this book does it doublely so for Node.js.

## Chapter 1- Node.js Design Fundamentals

Node.js was not designed to solve a scalability problem, but to solve threads being idle while waiting for I/O. Its strength is passing data to many clients. In a [recent interview with Netflix](https://www.talentbuddy.co/blog/building-with-node-js-at-netflix/), it is mentioned that _for the same function_ (I believe for the frontend Netflix), switching to Node.js from Java reduced the requirements for Amazon EC2 resoures by 75%. This makes sense as in the front end, you are probably just looking up (in a database or internal API) recommendations for a specific user. On the other hand, it also exemplifies using the right tool for the job.

1. Since Javascript utilzies the __synchronous event demultiplexer__ mechanism for its nature (and event loop), using synchronous code excessively would defeat the many benefits of Node.js.
2. The reactor pattern, libuv (a C library that makes Node.js compatible with all the major platforms for the Event Demultipleer), V8 JavaScript engine, __node-core__ (high level Node.js API), and code connecting libuv to JavaScript are the building blocks of Node.js
3. Realization- callbacks (defined as "function passed as an argument to another function B and is invoked when B is done ") work naturally in Node.js due to implicit closures in JavaScript. (And callbacks is called "continuation-passing style" in functional programming).
4. Throwing in async callbacks will cause an exception to jump to the event loop --> use try-catch blocks (page 29 for example)
5. Continuing after uncaught exceptions may leave the application in an inconsistent state, hence the importance of having solid tests in Node.js
6. Node.js modules are built with the CommonJS modules specifications
7. Observer pattern and Event Emitters vs Callbacks


## Chapter 2- Asynchronous Control Flow Patterns

In Chapter 2, the author starts with callback hell with a particular focus on the readability of the code. As some say 50-70% of engineer time is spent on reading code, writing readable good is very important. Instead of directly diving into promises and async libraries (and ES6 promises and factories are discussed later), the author first refactors the same code using plain old ES5 javascript through best practices: reducing if/else by returning <code>callback(err)</code> and factoring out reusable pieces.

