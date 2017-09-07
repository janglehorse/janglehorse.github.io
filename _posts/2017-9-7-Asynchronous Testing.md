---
layout: post
title: What I learned about asynchronous testing with Vertx unit  
---

A few weeks ago, I finished up a task in our API in which touched the 3 major
components of our codebase. I had to write a new endpoint for a DELETE on an asset,
write a db method for that endpoint to call, and create tests.
I won't lie, it was daunting, but it was great getting my hands dirty and taking a deep
dive into our codebase.

Writing test logic was more or less straightforward since we have a pretty robust test suite.
Error handling was certainly a learning curve, but again, I had a lot of
code to reference for this. The trickiest part by far was understanding when
each piece of code was being executed.

**The Async object**

The key to getting tests right was understanding the Async object. Essentially, when calling
an asynchronous method, `async.complete()`, or `async.countdown()` must be invoked to tell Vertx unit to wait
for the asynchronous result. If this is not done, timeout errors will follow, or worse, the test will "pass" by completing
before any asynchronous results have come back, and at that point __I might as well ask my 2 year old to test my code__. 

Sources: <http://vertx.io/docs/vertx-unit/java/>
