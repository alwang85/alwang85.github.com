---
layout: post
title: "Thoughts on book: Node.js Design Patterns   part 2"
description: ""
category:
tags: []
---

## Chapter 7- Scalability and Architectural Patterns

Summary- Reasons to scale includes workload, availability, and tolerance to failures. The Scaling Cube has an X Axis of cloning, Y Axis of decomposing by service, and z axis of splitting by data pattern. Z axis is usually done after X and Y are done- through horizongtal partitioning / sharding.

### Cloning and Load Balancing

Since Node.js processes are single-threaded and have a memory limit of 1.7GB on 64 bit machines, scalability is usually considered earlier on by Node.js Engineers.


A simpler implementation of cloning starts with the built in Node.js <code>cluster</code> module. The default after Node.js 0.11.2 leverages a round robin algorithm that assigns processes one by one. Using plain old JavaScript, it is possible to increase availability through reliency by restarting cluster workers upon error/existing. We can also write custom functions that restart workers one by one to have zero-downtime or performs load balancing. By default, additional threads on the same computer share the same port / memory.

### Dealing with Stateful communications

When we have several application instances, how do we maintain stateful communications between a client? One method is to share the state across a database or leverage Redis/Memcached. Another is by sticky load balancing- once a session starts, that session is assigned to the same instance determined by an algorithm (based on location, username, IP etc).

Alternatively, if we have several machines running multiple instances, and then use a reverse proxy to provide one single entry point for external communications. Popular reverse proxies such as Nginx not only act as a reverse proxy, but can also support load balancing, stick yload balancing, route to any available server regardless of language, URL rewrites, caching, and serving static files.

### Load Balancing and Scaling

<code>forever</code> and <code>pm2</code> are popular Node.js modules that can keep Node.js processes alive by auto restarting. When a Service Registry is implemented, load balancing between different microservices and dynamically scaling the microservices instances becomes possible. Alternatively, peer-to-peer balancing is sometimes used when we don't need a reverse proxy to hide the complexity of the app and all server instances are known (such as internal systems where requirements are pretty much static).

 ### Application Architecture

A monolithic architecture is when every module is part of the same codebase and runs part of a single application. We can create microservice architecture by breaking down the services each connected to separate databse instances (data ownership of each service). If one service crashes, some of the other services would still continue to work as normal. Also, if we decided to rebuild different services from scratch, it is much easier to do so for a microservice. If the services are accessed through a similar protocol (like a RESTful web service), the services can be programming language, database, infrastructure agnostic instances, allowing for the best tools for the job.

Challenges of the above include higher complexity in integration, deployment, and code sharing. Deploying, Scaling, and Monitoring the separate services become more difficult. Many DevOp and Cloud services help mitigate the problems, but <code>Seneca</code> and <code>nscale</code> are popular Node.js solutions specialized for this purpose.

### Integration Patterns

API Proxy- a server that basically acts like a reverse proxy and a load balancer for different services.

API Orchestration Layer - an abstraction layer that takes generically-modeled data elements and/or features and prepares them in a more specific way for a targeted developer or application. For example, a "completeCheckout" Event in API Orchestration could use the payment service, empty the cart service, and update product qty. While this is easy to design/scale, it also creates an anti-pattern called God Object, which knows and does too much.

Message Broker - A publish/subscribe pattern, when events in one service are emit to the broker, and the event is then broadcasted to other services to perform the appropriate transactions.
An interesting follow-up is how to handle load balancing with such event emitters, and that's the topic of chapter 8






