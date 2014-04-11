[Realtime predictive analytics using scikit-learn & RabbitMQ](https://us.pycon.org/2014/schedule/presentation/224/)

@beckerfuffle

[beckerfuffle.com]

[slides](github.com/mdbecker)

As a data guy, he doesn't really do much math; `from sklearn import SVC`
is really all ya need.

This talk isn't particularly well-organized, but the slides have tons of
example code that will probably be a lot more informative than these
notes. Or than the talk itself.

Scikit-learn Overview
=====================

Salient points from this section:

- ngrams
- tfidf
- overtraining

So, basic machine learning; supervised learning model, get all the data.
Just like what we talked about in the last machine learning thing!

So, simple model: take a tfidf vectorizer, throw it into a pipeline,
load up a classifier from sklearn, and let it do the magic.

sklearn has a lot of tools for figuring out which parameters are best
for all the various functions it gives you. Using sklearn to figure out
how to best use sklearn! I love it.

One interesting point that was brought up in questions: the size of the
data! The examples all used very large amounts of data, and the model
was trained on large amounts of data. It is rather inaccurate; would
smaller training sets help with this?

Also worth noting that he chose the examples he did because some of the
languages used the same character set; otherwise it would be easy.

Model Distribution
==================

Okay, let's say you've got a great model all figured out, using all the
valuable tools you learned in the last machine learning talk.

Everyone seems to use pickle for distributing the model, but that's
clearly dumb. Pickle is still the recommended way of serializing the
model according to the scikit people.

Data Flow
=========

Okay, so you've got data streaming in and being asyncronously processed.
This example application uses polling.

RabbitMQ
========

Woooo a queue. Is it a good one? Who knows? It uses AMPP. The slides
have some examples from which you can probably find better
documentation. But the details don't really matter, a queue is a queue.

Scalability
===========

A lot of scikit-learn scales linearly.

Standard scaling problems and solutions apply here.

Conclusion
==========

> A predictive model is like a piano. If it's not in tune, it's gonna
> suck.

So how do we make sure to keep this in tune? Allowing users to report
problems, re-training on occasion, no real good automated solution.

Ooooh, really cool idea: train a classifier to identify new vs old data.
The more accurate the classifier is able to get, the more outdated your
data is.
