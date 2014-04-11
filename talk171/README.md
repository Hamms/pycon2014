[Straightening Out AngularJS with Python](https://us.pycon.org/2014/schedule/presentation/171/)

hehe, this guy's last name is pronounced "Skank"

Backbone is still [pretty
dominant](http://www.google.com/trends/explore#q=angular.js%2C%20ember.js%2C%20backbone.js)

What We Serve
=============

So, we start by just serving a basic html page. For everything. Angular
itself handles the routing. The way angular in particular works is by
providing a superset of HTML with the templating in there, as opposed to
Ember which has HTML-looking templates as special scripts.

Angular also lets us serve up template partials so we don't have to load
everything in one go. Like we do with Ember. (Is something like this
possible in ember?). Easy to do this in lots of different ways; purely
static, with some serverside magic, with lots of serverside magic,
whatever.

Most interestingly, we have to connect to the server! This leads us
naturally to ...

Application API
===============

There are two kinds of APIs: application apis and developer apis.
Sometimes those lines are blurred, but the basic idea is that an
application api is going to be consumed by your application, the
developer api is going to be consumed by other developers or other
libraries or what have you. Today, we're only talking about the former.

So we want a clean, RESTful JSON api. Lots of tools out there to help
with this, but also still a long ways to go with developing the tools.

A super-basic API using something like django REST framework is about as
simple as you'd expect.

> And the world would be a beautiful place if that was all you ever had
> to do.

But what about all those inevitable edge cases?

Annoying Shit
=============

Cookie-based authentication is still the default mode for a lot of
applications. Token-based authentication (`JSON Web Tokens`) has a lot
of advantages as well, but we're talking today about cookie-based
(damn).

So we're going to want a custom POST endpoint for authentication. And
here in the slides we see a typical first draft login route. I must have
written a view like this at least a dozen times.

> And don't even get me started on the whole password reset workflow.
> It's messy and gross.

And of course we want permissions! Users should only be able to see
stuff they're allowed to see, and of course should only be able to
modify stuff they own or are allowed to. So a super-naive implementation
is shown, but obviously a more generic permissions system is required.
You pretty much have to do all this stuff by hand.

Then of course you want filtering! Again, at least with Django REST
Framework, you have to write this shit by hand. Or you could go with
something like Flask-Restless but we all know what happens when you go
that route.

All in all, there's a ton of shit to do.

Curveballs
==========

Lots of little annoyances here. CSRF, Pagination. A couple bigger ones:

`MMVV**`
--------

So what happens when you have an MV\* In the backend and we want an
analogous MV\* in the backend? Well, we've gotta mirror our backend
models in the frontend. Fortunately, this pattern means that the backend
doesn't really need much in the way of the "V\*" side of that, since the
frontend is doing the really fun stuff.

However, there will still be quite a lot going on in the backend.
Angular and the like aren't for data crunching.

Interpolation!
--------------

The problem we encountered with Jinja/Ember, hence that special importer
that Drew wrote. This can be handled with Angular by overriding the
clientside syntax.

Conclusion
==========

This is actually a good space for more tooling. It's a newer space than
most, and there are obviously still many problems without solid generic
solutions. We definitely have the potential to make a positive impact
here.

Also, holy shit, Pyramid has this auth stuff built in??

