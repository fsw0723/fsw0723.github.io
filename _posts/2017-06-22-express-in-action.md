---
layout: post
title: "Express in action 读书笔记"
date: 2017-06-22 13:54:00 +0800
categories: front-end
---

Just finish reading **Express in Action**. Some highlights here.

## Part 1: Intro

### 1. What is Express?

* Express is a relatively small framework that sits on top of Node.js’s web server functionality to simplify its APIs and add helpful new features. 
* Express is a minimal, unopinionated framework that’s flexible.
* Express has a few key features:
    * **Middleware** which is a way to break your app into smaller bits of behavior.
Generally, middleware is called one by one, in a sequence.
    * **Routing** similarly breaks your app up into smaller functions that are executed
when the user visits a particular resource; for example, showing the
homepage when the user requests the homepage URL.
    * Routers can further break up large applications into smaller, composable
**subapplications**.

* Most of your Express code involves writing request handler functions, and
Express adds a number of conveniences when writing these

### 2.The basics of Node.js

Node.js (often shortened to Node) is a JavaScript platform based on Chrome v8 engine.
It has nature of **asynchronous**.

### 3. Foundations of Express

* Express sits on top of Node’s HTTP functionality. It abstracts away a lot of its
rough edges.
* Express has a middleware feature that allows you to pipeline a single request
through a series of decomposed functions. 
![express middleware](/assets/express-in-action/middleware.png){:class="img-responsive"}

    Some third-party middleware libraries:
    
    * **Morgan**: Logging middleware
    * **Express's static middleware**
    * **connect-ratelimit**: Lets you throttle connections to a certain number of requests
    per hour. If someone is sending numerous requests to your server, you can start
    giving them errors to stop them from bringing your site down.
    * **Helmet**:Helps you add HTTP headers to make your app safer against certain
    kinds of attacks.
    * **cookie-parser**: Parses browser cookies.
    * **response-time**: Sends the X-Response-Time header so you can debug the performance
      of your application.
* Express’s routing feature lets you map certain HTTP requests to certain functionality.
For example, when visiting the homepage, certain code should be run.
* Express’s view-rendering features let you dynamically render HTML pages.
* Many templating engines have been ported to work with Express. A popular
one is called EJS, which is the simplest for folks who know already HTML.


