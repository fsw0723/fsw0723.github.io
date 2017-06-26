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
   
* Express’s routing feature lets you map certain HTTP requests to certain functionality.
For example, when visiting the homepage, certain code should be run.
* Express’s view-rendering features let you dynamically render HTML pages.
* Many templating engines have been ported to work with Express. A popular
one is called EJS, which is the simplest for folks who know already HTML.

## Part 2

### 4. Middleware

* Express applications have a middleware stack. When a request enters your
application, requests go through this middleware stack from the top to the bottom,
unless they’re interrupted by a response or an error.
* Normal middleware
{% highlight javascript %}
    app.use(function(req, res, next) {})
{% endhighlight %}
  Error-handling middleware
{% highlight javascript %}
    app.use(function(err, req, res, next) {
     console.error(err);
     next(err);
    });
{% endhighlight %}
    
* There are numerous third-party middleware written for your use. Many of these
are maintained by Express developers.
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
    * **connect-assets**: Compiles and minifies your CSS and JavaScript assets. It will also
        work with CSS preprocessors like SASS, SCSS, LESS, and Stylus, should you choose
        to use them

### 5. Routing

* Routing is a mapping of an HTTP verb (like GET or POST) and a URI (like
/users/123).
* Routing can map to a simple string. It can also match against patterns or regular
expressions.
* Express has the ability to parse query strings.
* As a convenience, Express has a built-in middleware for serving static files.
* Routers can be used to split your application into many smaller applications,
which is useful for code organization.
* You can use Express with HTTPS by starting the server with your certificates.
{% highlight javascript %}
var httpsOptions = {
 key: fs.readFileSync("path/to/private/key.pem"),
 cert: fs.readFileSync("path/to/certificate.pem")
};
https.createServer(httpsOptions, app).listen(3000); 
{% endhighlight %}

### 6. Building APIs

### 7. Views and templates: Pug and EJS

* 
{% highlight javascript %}
var express = require("express");
var path = require("path");
var ejs = require("ejs");
var app = express();
app.locals.appName = "Song Lyrics";
app.set("view engine", "jade");
app.set("views", path.resolve(__dirname, "views"));
app.engine("html", ejs.renderFile);
app.use(function(req, res, next) {
 res.locals.userAgent = req.headers["user-agent"];
 next();
});
app.get("/about", function(req, res) {
 res.render("about", {
 currentUser: "india-arie123"
 });
});
app.get("/contact", function(req, res) {
 res.render("contact.ejs");
});
app.use(function(req, res) {
 res.status(404);
 res.render("404.html", {
 urlAttempted: req.url
 });
});
app.listen(3000);
{% endhighlight %}

The three cases of calling `render`:
1. Express builds up the context object every time you call render.
2. You decide whether view caching is enabled. 
{% highlight javascript %}
app.enable("view cache")
{% endhighlight %}
3. You look up where the view file resides and what view engine to use. 
4. If you don’t supply a file extension (as with about in the previous step) Express appends the default you specify.
5. Express looks at your file extension to determine which engine to use.
6. Express looks the file up in your views directory. 
7. Express caches all the lookup logic if it should.
8. You render the view. 

* consolidate.js
* The EJS templating language is a light layer on top of HTML that adds the ability to dynamically generate HTML with pieces of JavaScript.
* The Pug templating language is a reimagining of HTML that lets you dynamically render HTML with a whole new language. It attempts to remove verbosity and typing.

## Part 3: Express in Context

### 8. Persisting your data with MongoDB
* Mongo is a database that lets you store arbitrary documents.
* **Mongoose** is an official Mongo library for Node. It works well with Express.
* To securely create user accounts, you need to make sure you never store passwords
directly. You’ll use the **bcrypt** module to help us do this.
* You’ll use **Passport** to authenticate users, making sure they’re logged in before
they can perform certain operations.

### 9. Testing Express applications
* Unit test: **mocha** and **chai**
* **SuperTest**

### 10. Security
* Using a syntax checker like **JSHint** can help you spot bugs in your code.
* Parsing query strings in Express has a few pitfalls. Make sure you know what
variable types your parameters could be. **arraywrap**
* HTTPS should be used instead of HTTP.
    * Force users to HTTPS: **express-enforce-ssl** 
    * Keep users on HTTPS: Add header **Strict-Transport-Security** (**helmet)
* Cross-site scripting, cross-site request forgery, and man-in-the-middle attacks
can be mitigated. Never trusting user input and verifying things each step of the
way can help secure you.
    
  Solution: **helmet**, Add CSRF token (**csurf**)
* Crashing servers is a given. **Forever** is one tool that you can use to make sure
your application restarts after a failure.
* Auditing your third-party code using the Node Security Project (and common
sense!): **nsp audit-package**
* Various little tricks
    * No Express here: 
    {% highlight javascript %}
app.disable("x-powered-by")
    {% endhighlight %}
    * Preventing clickjacking:    
    {% highlight javascript %}
app.use(helmet.frameguard("sameorigin"));
app.use(helmet.frameguard("deny"));
    {% endhighlight %}
    * Keeping Adobe products out of your site
    {% highlight html %}
<?xml version="1.0"?>
<!DOCTYPE cross-domain-policy SYSTEM "http://www.adobe.com/xml/dtds/cross-domain-policy.dtd">
<cross-domain-policy>
 <site-control permitted-cross-domain-policies="none">
</cross-domain-policy>
    {% endhighlight %}
    * Don't let browsers infer the file type
{% highlight javascript %}
app.use(helmet.noSniff());
{% endhighlight %}

### 11. Deployment: assets and Heroku
* **LESS** is a language that compiles to CSS. It adds a lot of conveniences like variables
and mixins.
* **Browserify** is a tool for packaging JavaScript to run in the browser. It packages
files so that you can use Node.js’s module system in the browser, allowing you to
share code between your client and your server.
* **Grunt** is a generic task runner that can do lots of things. One of the things
you’ll do with Grunt is compile CSS with LESS and package JavaScript with
Browserify.
* **connect-assets** is an alternative to Grunt in some ways and allows you to compile
CSS and JavaScript using Express middleware.
* **Heroku** is one of many cloud application platforms that allow you to easily
deploy your Express applications to the real world.

### 12. Best practices
* Simplicity is a high-level goal for software in general. You should be rigorous
about removing complexity in your software.
* There is a folder and file structure that emerges for most Express applications.
![Express file structure](/assets/express-in-action/file-structure.png){:class="img-responsive"}    
* For maximum reliability, you should lock down the versions of your dependencies.
This has some disadvantages—namely, you won’t be automatically running
the latest and greatest code—but it has the advantage that your code won’t be
automatically upgraded without your knowledge. （npm-lock.json）
* Installing dependencies locally will help keep your system clean and your projects
reproducible. You’ll use npm scripts to do this.