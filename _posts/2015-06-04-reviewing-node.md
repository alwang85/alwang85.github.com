---
layout: post
title: "Reviewing Node"
description: ""
category: 
tags: [node, nodejs, Node.js]
---
{% include JB/setup %}

## Overview

### What is Node.js?

As per the website, Node.js is a platform based on Chrome's Javascript runtime for building fast , scalable network applications. Node.js uses an event-driven, non blocking I/O model making it perfect for data-intensive real-time applications that runs across distributed devices. It was written in C++ and can work with C/C++ Libraries.

Node.js has many built in modules, and may be expanded with Express.js for more advanced web applications. Some modules need to be imported by _"var x = require('X')"_. Node.js is the N in MEAN stack for MongoDB, Express, Angular, and Node.

## Commonly used node modules

### Helpers

[fs](https://nodejs.org/api/fs.html) - require('fs') - provides file I/O

[os](https://nodejs.org/api/os.html) - require('os') - provides info about hardware + os

[path](https://nodejs.org/api/path.html) - require('path') - path related helper

[dns](https://nodejs.org/api/dns.html) - require('dns') - resolves ip/dns related records

[process](https://nodejs.org/api/path.html) - global - provides info about the node process

[timers](https://nodejs.org/api/timers.html) - global - allows setTimeout etc


### Encode / Decode

[crypto](https://nodejs.org/api/crypto.html) - require('crypto') - hashing stuff

[query-string](https://nodejs.org/api/querystring.html) - require('query-string') - parse, encode, stringify URL query strings

[url](https://nodejs.org/api/url.html) - require('url') - url parser

### Server

[http](https://nodejs.org/api/http.html)- require('http') - built in simple http server (check out https)

[net](https://nodejs.org/api/net.html) - require('net') - server for streams

[event](https://nodejs.org/api/events.html) - require('events').EventEmitter - a server side event emitter

[cluster](https://nodejs.org/api/cluster.html) - require('cluster') - allows Node to use multi-cores - unstable

### Debugging / Testing

[util](https://nodejs.org/api/util.html) - require('util') - debugging

[assert](https://nodejs.org/api/assert.html) - require('assert') - unit testing

[console](https://nodejs.org/api/console.html) - global - console.log prints output, console.time / console.timeEnd is helpful

[debugger](https://nodejs.org/api/debugger.html) - global - debugger


### Other

[zlib](https://nodejs.org/api/zlib.html) - require('zlib') - zipping streams

## Node Classes
1. Buffer
2. Streams

