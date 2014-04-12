[Writing RESTful web services with Flask](https://us.pycon.org/2014/schedule/presentation/221/)

By the guy who wrote the Flask mega-tutorial!!

Basic APIs in Flask
===================

boring boring boring boring

Advanced APIs in Flask
======================

Authentication
--------------

There are many things you always need to do; they're the same for every
project. For this, he has written Flask-HTTPAuth which provides a simple
decorator which requires password auth. And a login required. Blah blah,
we're already doing all this.

    @auth.verify_password
    def verify_password(token, password):
        g.user = User.validate_auth_token(token)
        return g.user is not None

You can also do global API Protection with Flask's `before_request`
handler. Simply:

    @api.before_request
    @auth.login_required
    def before_request():
        pass

You can use tokens or passwords. You can use itsdangerous, lots of shit.
This was an incredibly simplistic overview of authentication.

Automatic JSON Responses
------------------------

These examples are all using his own decorators, but the real power of
flask comes from defining your own decorators

For example, rather than calling `jsonify` and `to_json` all the time,
we can simply create a decorator to do that for us.

    def json(f):
        @functools.wrap(f)
        def wrapped(*args, **kwargs):
            rv = f(*args, **kwargs)
            if not isinstance(rv, dict):
                rv = rv.to_json()
            return jsonify(rv)

Again, super-simple. Let's do something fun.

Rate Limiting
-------------

Now this sounds interesting.

    @rate_limit(limit=5, per=15) # maximum of 5 requests per 15 seconds

The full code is in the slides, but again it is a simple decorator. In
this case, using Redis for storage and returning 429 in the offending
case.

Lots of other boring stuff
--------------------------

Basically, he just uses a bunch of decorators and functional views
rather than class-based views and mixins. Six of one.

eTags
-----

Okay, this is the one interesting thing. Basically, we have a route that
the client can query to ask if the data is still the same .... we just
return an MD5 of the data and use the appropraite headers to let the
client check if the data it has is still valid. This is cool; we should
definitely use this.


