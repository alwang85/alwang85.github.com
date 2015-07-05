---
layout: post
title: "book  Practical Node.js"
description: ""
category: 
tags: []
---
{% include JB/setup %}

# Overview

"Practical Node.js" is a well written book by _Azat Mardan_. It starts chap1 with the basics of Node.js and useful utilities. Chap2 introduces building express apps with the built in generator and common middleware, and without the generator. The third chapter talks about various TDD/BDD frameworks such as Mocha, Assert.js, and Expect.js. Chap4 was about server side rendering with jade and handlebars. Chap5 was an intro to persistence with MongoDB and Mongoskin. Chap6 was using sessions and oauth to authorize/authenticate users. Chap7 is using the Mongoose ORM library. Chap8 is building RESTful API servers with express/hapi. Chap 9 talks about websocket, socket.io, and derbyJS. Chap10  was preparing apps to become production ready. Chap11 is about dpeloying apps. Chap 12 is about contributing to open source.

While alot of the book for me personally was review, I think this is a wonderful book for people looking to know more about fullstack Javascript.

### Mongoose, Mongoskin, and comparing libraries

Having familiarized myself with the Mongoose ORM library before spending much time with the native MongoDB driver and Mongoskin, I greatly appreciate the elegance the ORM library brought. That said, when comparing libraries of a similar nature it is important to understand the syntax. For example, I think of Mongoose collection representations as <code>Messages.findOne({})</code>, while the raw MongoDB driver example was <code>db.collection('messages').findOne({})</code>. The first is clearly less verbose than the later, however if for the later we set an alias of <code>var Message = db.collection('messages')</code>, that would have brought the different libraries to a similar conciseness under the context.

Of course, Mongoose isn't an ORM layer due to its conciseness in syntax. NoSQL databases don't have schemas themselves. By using an ORM layer on the Node.js instances, we shift the database side validations/functions to the Node.js instances, levaraging the scalability of Node.js apps and reducing the need of database/server instances to handle a similar amount of database transactions. This is important, as scaling the Z-axis on the scalability scale is the most expensive.

### Websockets, socket.io, and other frameworks

The chapter about real time apps using native html5 web sockets, socket.io, and a framework such as derbyJS was interesting. Socket.io is a great library as it has multiple fallback methods for browser compatability. I have to admit, I got hooked to the game [agar.io](www.agar.io) for a few days. When I witnessed the Friday night lag, all I could think of was how scalable was the app given decent FPS? How much computation is handled client side vs server side? Quick research suggested vector data is sufficient (direction + speed sent on change) vs actual location (constant polling required). I considered creating a clone of agar.io for fun, however a quick search on agar.io on github found many results, with a popular clone repository with many people working together to improve the clone. A specific [open issue](https://github.com/huytd/agar.io-clone/issues/188) that interested me was the replacement of socket.io. There were discussions on which library/technology should be used as the replacement, and an article about [optimizing websocket bandwith](http://buildnewgames.com/optimizing-websockets-bandwidth/) popped up.

The gist was, socket.io converts items to JSON format, while different libraries sending simple binary data could be potentially half the message length. When the network bandwidths are the bottleneck, it makes sense to use socket technology with a smaller footprint. The concensus in the discussion thread seemed to try the <code>ws</code> library. I really loved reading people's comments and thoughts on a technical challenge I was interested into as well.

Frameworks like DerbyJS and Meteor.js have interesting built in capabilities, and Firebase is also nice for syncing databases. Many different tools for different cases.

### Getting Node.js App Production Ready

This was a great and practical chapter:

 1. Setting environmental variables on any node process
 2. Conditional error handling in Express.js based on NODE_ENV
 3. How to share the in memory store like Redis on different Node.js processes/servers
 4. Setting socket.io to production
 5. Leveraging hipchat/twilio/sendgrid etc to send notifications on server errors
 6. Using the 'domain'' library to trace errors
 7. Multithreading with Cluster and Cluster2 (ebay's production library)
 8. Creating an api route that functions as a dashboard of the process
 9. Different processes with Grunt
 10. Continuous Integration with  cloud testing with TravisCI and codeship

 ### Conclusion

 This was a wonderful book to help build real-world scalable web apps with best practices and scalability in mind. I really enjoyed the variety of topics covered in this book, along with the up to date best practices of the respective best in class Node.js specific libraries. The other wonderful book I'm still reading is "Node.js Design Patterns" has some more in depth examples and use cases, however is more difficult to digest at once due to lots of theory + depth. With these 2 books, and the myriad of modules available in the npm ecosystem, an informed engineer can do so much to leverage the advantages of Node.js.






