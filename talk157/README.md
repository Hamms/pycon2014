[By Your Bootstraps: Porting Your Application to
Python3](https://us.pycon.org/2014/schedule/presentation/157/)
@tresseaver

Porting Strategies
==================

Originally, everyone thought that we could just port everything. That
doesn't work, so `2to3` was conceptualized, which it turns out is
*painfully slow* on large codebases.

So the best solution? Straddling! A single codebase that works on both
major versions. Using a compatible subset, conditional imports, and
`six` when necessary.

Targeting Python Versions
=========================

Syntax changes make python2 < 2.6 hard. No `b''` literals, no `except
Exception as e:`. So if you care about older versions, (thank god we
don't) then things get interesting.

"2.6 is the bare reasonable minimum."

Incompatibilities make Python 3 < 3.2 hard; `u''` literals don't show up
until 3.3, `callable()` shows up in 3.2. Plus, some WSGI shit was broken
pre-3.2, so 3.2 is really the minimum; 3.3 isn't sufficiently
distributed yet.

In short: 2.6+, 3.2+

Managing Porting Risks
======================

Woooo, bugs! The big fear of porting is that by adding python3 support
you run the risk of breaking python2 support. So how do we get more
confident?

*Testing!* Testing is good. Always test. We should write more tests.

More modern python2! I'm not sure what he means by this. Idioms? Sounds
like that book on porting python3 that I picked up might have more
information on this. The python wiki also has some more
information/examples about this.

Be more clear about text vs bytes. (Fortunately not an issue for us)

Bottom-Up Porting
=================

You can't port something until the dependencies have been ported! So you
gotta find the packages in your stack that need to be ported that don't
depend on things that haven't been ported. Topo sort!

Iterate until you're done, then you can port your application.

Common Subset
=============

Running `python2.7 -3` can point out problem areas.

DON'T USE BARE-STRING LITERALS. Use `u''` for everything.

holy shit, print isn't a statement anymore! It's a function!

You can use `except .. as ..` as well as `__future__` imports.

Testing!
========

Testing testing testing testing.

Unit testing preferable for libraries.

Functional testing best for applications.

You can measure coverage with the
[`coverage`](https://pypi.python.org/pypi/coverage) module on pypi. In
addition to coverage, you have to make sure that your assertions make
sense; you should always be asserting actual contracts, not
implementation details.

Doctests tend to assert implementation shit rather than inherent shit;
think of them more as documentation with examples. They let you test
your documentation but not your code, and can/should probably be
converted to Sphinx examples.

Tox seems like a cool way to automate testing. His implementation uses
nosetests as well as sphinx-build. It bundles your code as a package and
installs it into a virtualenv for each version of python that you're
testing.

C Extension Stuff
=================

This is more difficult 'cause it's C. Fuckin' C. Thank god we don't
care, but that book again has some cool stuff to say.

Python reference implementation is ieasier

Hygeine Issues
==============

Trove classifiers! What are those?! They let you "signal" supported
versions, whatever that means.

Bump major version for backwards compatibilitiy.


Resources
=========

python3porting.com
testrun.org/tox/latest

