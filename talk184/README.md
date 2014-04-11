@heddle317


A Typical Python Web App
========================

Standard shit. Database, web server, all running on a server.

But then you want logging! Log files on the machine are a quick, easy
way to do it. Then you want version control, so git/github,
svn/bitbucket. Then you probably want some async task handling, so
pythonrq or celery or something like that. You can also use async
frameworks like twisted or tornado.

How about exception handling! Emails are a great way to start, so you
gotta run an smtp server.

So this thing is getting pretty big, so we gotta start pulling shit into
different servers. Namely, you split your DB out onto another server and
set up a cache to handle data people use a lot, so you use memcached,
redis, etc. After that, you'll probably have to pull out your async
tasks, exception handling, and logging out into external
servers/services.

And then of course the final step is replication! Single points of
failure are BAD, so there are tons of patterns here for sharding,
read/write servers, etc.

So next up! We have the "system of systems." At some point, you need to
build yourself a development environment while you're going through this
whole process. You want dev to be as close as possible to production.
venv, vagrant, etc. Of course, because you're a good developer, you've
written tests so you want to run them automatically so you add in a
testing layer (jenkins, circleci, travisci). And of course you have
multiple dev environments, so you need yourself a staging environment
that everyone pushes to for the testing shit.

Now you have production, testing, staging, and dev environments that all
need to be identical, so you need yourself some automatic server
configuration, as well as deployment for handling all the multiple
servers.

The final level of the "system of systems" is where you need this system
for all your different services. Your async tasks, your exception
handling, your application, etc. Woooo recursion.


Stages of Development
=====================

Dev
---

Staging
-------

Production
----------

Deploy
------

Helpful Python Libraries
========================

https://github.com/heddle317/django-chef-application
https://github.com/heddle317/full-stack-resources

Notes
=====

Look up more on twisted and tornado
