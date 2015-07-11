---
layout: post
title: "Tried Meteor.js through a Slack clone tutorial"
description: ""
categories: [post]
tags: []
---

At scotch.io I found an intro to [Meteor.js](https://scotch.io/tutorials/building-a-slack-clone-in-meteor-js-getting-started) tutorial through creating a Slack clone. There were some unclear instructions in where code was to be placed etc, but it was decently easy to debug when you cross reference the comments and source code. Links to my [repository](https://github.com/alwang85/ember_slack) and [live site](http://alwang85-slack.meteor.com/random).

Syntax stuff aside, there were a few interesting differences compared to the MEAN stack:

1. Meteor.js is both server side code + client side code
2. In Node I'm used to declaring file depencies, while Meteor.js loads many files automatically (and alphabetically), making naming very important for non-special directories (client/, server/, public/, private/, test/)

## Gems

Meteor.js has its own 'gems' packages ecosystem. By typing <code>meteor add accounts-base accounts-password accounts-ui</code>, by default it inserted a User collection in Mongo, and you just need to add <code>{{> loginButtons}}</code> to show the login functionality.

Setting up github oauth as was simple as:

<code>meteor add accounts-github</code>

Configuration of github-oauth (yes, a GUI!):

![configuring github settings](http://i.imgur.com/fOlbJek.png)

And that's it!


## Built-in Stuff

Reactivity- detecting changes in a data source and then recomputing the values, publishing them to client side automatically

Minimongo- a local version of mongod that works offline, integrated with the mongo server

Latency Compensation- Updates UI without server confirmation, changes UI only if needed when server responds

Auto pub-sub to all clients (for rapid prototyping, authentication is very important step)

Simple deployment to Meteor.com through <code>meteor deploy app-name.meteor.com</code>


## Conclusion

Disclaimer: Since I was just using Meteor.js through a tutorial designed to highlight the benefits of Meteor.js, I can't really speak to anything conclusive. Here's what I experienced:

Pro's of Meteor.js: Built-in real time syncing and allowing offline usage/latency compensation through minimongo was cool. Easy integration with MongoDB and creating collections on the fly, also easy to seed database.

Confusing parts of Meteor.js: Requires alot of discipline in naming files for load order (compared to explicity dependency injection in AngularJS), differentiating between server side, client side, and shared code.

While I am more used to Angular's dependency injection and relying on only RESTful API's as connections to the server, Meteor.js has a healthy-ecosystem, and really amazed me in how fast potentially it took to prototype a real-time app with client/server-side database caching. I am interested though in also creating an Angular version of a slack clone that offers reactivity, latency compensation, and pub-sub to get a feel for it.
