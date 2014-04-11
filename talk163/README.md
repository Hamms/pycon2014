[Enough Machine Learning to Make Hacker News Readable Again](https://us.pycon.org/2014/schedule/presentation/163/)

@nedjl / njl@njl.us / www.njl.us
[slides](http://www.njl.us/talks/enough_machine_learning)

Machine Learning
================

Building statistical models of a bunch of input data for fun and profit.

Workflow:
- get data
- engineer data
- train/tune models (this is the science part)
- apply model

So scikit-learn is a great library for it. Requires scipy, but that's
the only complex part of the whole dang thing.

Big problem with machine learning? Too much terminology. The cheat sheet
he presented in the talk (TODO find this) help boil down what to google
for.

Scikit-Learn
============

It's got some cool patterns!

First thing you wanna do is create a validation set. After all, your
goal is to take a bunch of data the computer's never seen and teach it
how to infer stuff. So you take about 25% of your data, set it aside,
don't touch it at all, and then look at it afterwards to see how well
you did. Pretty standard corpus handling shit.

You're also likely going to have pipelines! A series of
classifiers/parsers/whatever that pass data along. He's got some simple
examples in the slides.

Hyper-Parameters
----------------
 
`sklearn.grid_search` will let you tweak parameters to figure out the
best way to handle things.

Data!
=====

Gathering and organizing data is the most painful part, but there are
lots of cool ways to deal with it. The big problem comes with
translating words into numbers. The classic frut flies banannas quote is
a great example; it's grammatically extremely complex and difficult for
humans to parse, so let's say fuck grammar and just count! If we want to
include a hint of grammar, we can start talking about n-grams.

It's also valuable to introduce some grammatic normalization and "stop words"
(words that we know we don't care about). We can also notice that if a
particular article uses the word "bitcoin" twelve times and the average
usage of "bitcoin" is like one or two, then we know that this article is
REALLY about bitcoin, so we "boost" the bitcoin count a little bit.

Of course, word counts is only one of the many features. We can also
infer features like length or combine features to create other features.
Lots of options!

Conclusion
==========

You can check out the results at [hn.njl.us](http://hn.njl.us/).

20 years ago, anyone who wanted to use a red-black tree had to go and
write it themselves. Now, all that shit is just in libraries.

5 years ago, if you wanted to do machine learning, you had to write
things yourself. No more! The tools are out there to be played with. So
go play with them!

