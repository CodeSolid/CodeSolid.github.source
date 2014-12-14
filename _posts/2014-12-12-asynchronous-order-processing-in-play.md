---
author: John Lockwood
layout: post
title: "Asynchronous Order Processing in Play - A Proof of Concept" 
excerpt: "Digging into akka and Play RESTful APIs while waiting for user group to show up."
categories:
- Scala, Play, Akka

---
There's a project at a company I know that I thought would be a great fit for a Play application. For reasons too complex to go into here, no one will be working on this application any time soon, but to me it's still a simple but interesting problem.  The gist of the thing is this:

The company has a service that handles orders for [top secret thing].  This service has some limitations.  First, it writes the order request into a database in real time, then a separate process running hourly on a different system reads the orders and sends them to a partner for processing.  The output of the second process is opaque to our customers -- i.e., there's not a separate service that allows them to retrieve the status of an order.

Obviously an application like this is rife for improvements:

* Minimally, the team could expose an endpoint to report the status of the order.  Yes, the order wouldn't be ready for up to an hour or more after it's submitted, but at least the customer could check the status without calling support.

* Better yet, rather than batching orders to our third party vendor we could send them as they're received, and return a result as soon as we get it.  Of course, the downstream server is not under our control, it might be out of commission, etc., so we'd want to store enough information locally to be able to resend the order if it fails.  Picking a number out of a hat, the team's manager suggested that orders would be processed in ten seconds, rather than hourly.

Of course, ten seconds is still an eternity if you're a user who just clicked the submit button, so taking the idea a bit further and using Play / Akka for the solution, a few ideas come to mind:

* Once submitted, the order should be "received" (i.e. written to our "local" datastore) as soon as possible.  This could still be an asynchronous request, of course, the response should be less than 100ms after the request is received.  Cassandra could do this in a walk, but MySQL could easily handle our volume as well.

* If the partner that process the order is down / overloaded, etc., we should be able to report a possible delay to the user as soon as possible.  The [akka circuit breaker](http://doc.akka.io/docs/akka/snapshot/common/circuitbreaker.html) pattern provides an elegant solution to this problem.

* The order status page should update itself in real time if possible.  Some alternatives:
	* WebSocket on modern browsers, but degrade to F5 to refresh status on older browsers.
	* Comet sockets everywhere.

At this point, I need to better understand best practices for WebSocket / Comet services, since this idea may be untenable.  A proof of concept may be easy to stand up in Play, but our client almost certainly will not be a Play app, so the order status information needs to be available as a stateless service endpoint as well).  Probably at minimum we need [Graceful Web Sockets](https://code.google.com/p/jquery-graceful-websocket/) in there, and probably another trick or two.

I started working on some code for this while waiting for someone to show up at the first meeting of the [ScalaUserGroup.org](http://ScalaUserGroup.org), and inasmuch as nobody did, I made pretty good progress! I may post the code soon if I can make it generic enough to protect the innocent.