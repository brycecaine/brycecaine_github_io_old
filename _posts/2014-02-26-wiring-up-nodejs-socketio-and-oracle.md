---
title: Wiring up node.js, socket.io, and Oracle (Oracle?)
date:   2014-02-26
categories: node oracle socketio web development
comments: true
---

Yep, Oracle.  While Oracle wouldn't have been my first choice for this functionality, the data we had to work with existed in Oracle, so we had to use the tools we had.  Here are the details.

Over the last couple days, my student worker and I have been trying to figure out how to push data to the browser based on changes in an Oracle database table.  Our first thought was that we would have to use <a href="https://github.com/joeferner/node-oracle">a node-oracle package</a> we found on GitHub.  The package worked nicely, and we were able to get it working, but the drawback was that we had to set a setTimeout for node to query Oracle and retrieve the data we needed.  We knew this wasn&rsquo;t going to meet our needs for live data-pushing, but we didn&rsquo;t know of any other way. That is, until we talked to our DBA.

Our DBA said it sounded like a job for a database trigger.  I knew of triggers, but thought they wouldn&rsquo;t work in this case because we needed something to listen for a change and send an http request to a web application.  My excitement piqued when our DBA then mentioned the utl_http package that Oracle provides.  I gave our DBA the url we would be testing with, she set up the needed ACL (access control list), and we were off to the races to see if we could get this to hello-world.

The approach we took was to make a http post request from Oracle to our node server.  We set up node to handle the request and broadcast the post-request data to the browsers with open sockets to the node server.  After much experimenting and trial-and-error, we arrived at the following code (modified to exclude environment-specific information):

[gist](https://gist.github.com/brycecaine/9245496)
