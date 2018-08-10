---
layout: post
title: "Don't underestimate short-stack development"
tags: 
- development
published: true
---

Today's "full stack" developers have to work with an unbelievable
number of technologies.  Containerisation (docker, kubernetes, EC2),
databases (NoSQL, SQL, flat-file, full-text indexing systems), caches
(redis, memcached, etc), backend and frontend languages, build systems
(often separate for front and back), message queues, email, SMS... it
can be very daunting.

Each new technology added to the stack introduces another layer of
complexity. Another dependency. Something else to be managed,
maintained, honed, and ultimately debugged when things go bad. It adds
a new point of fragility.  It adds more overhead during development,
more mental burden on the developers that have to work with, and often
around, it.

Often these technologies are added without much forethought. Teams
dive into creating a miriad of microservices and SPAs because big 
companies praise how they helped them tackle large projects. Such
approaches are seen to be simple answers to age-old problems around
unweildy monoliths that are creaking under the strain of an
accretion of features.

I'm not going to get into the problems around picking microservices
when monoliths go bad. (Many other developers have written more
eloquently about it)[1]. Nor am I going to go into the problems
with Single-Page Apps, though there are many and all are valid.

But from a pure development viewpoint, I'd ask you to reconsider
short-stack development for your next project. What do I mean by
"short stack"? Well, first, let's take a look at a common stack
for a modern project. We'll go front-to-back here.

- React, probably with Redux, left-pad, and the 1000+ packages somehow appear in node_modules.
- Some form of CSS framework, probably PostCSS, maybe Sass.
- Webpack, or similar build system
- Nginx/Apache
- webapp
- cache
- database
- message queue
- background workers




1: https://www.simplethread.com/youre-not-actually-building-microservices/
