[Fan-in and Fan-out: The crucial components of concurrency](https://us.pycon.org/2014/schedule/presentation/218/)

@haxor / onebigfluke.com / [slides and more](github.com/bslatkin/pycon2014)

# Goal

So the big question: why do we need Tulip? Everyone's heard of it, no
one has used it.

It's pretty easy to do shit in python. But it's very hard to do many
different kinds of shit at the same time in the same program in python.

Note: we're not talking about CPUs, parallelism, locking, or any of that
shit. We're talking about concurrency.

# Definitions

Check out the slides.

# The Old Way

So, as an example, let's build a web crawler. Code in all in the slides,
but the general process is obvious. We fetch a url, find all the
urls on a page, and recurse breadth-first.

So in the naive implementation, this is extremely slow. It blocks, if
one site responds slowly, the rest of them will stall, it's just slow
and dumb. So how can we make it faster?

Threads! There are lots of other options to parallelize this; forking,
sockets, remote machines, tons of things that all have their own flavor,
but we'll talk about threads.

So `crawl_parallel` has nothing to do with crawling, so why are we
looking it? Well, it's spawning a bunch of instances of fetchr.

Woah, fetcher is crazy. It's a thread that never ends! Just spins
forever under a `while True:` loop. Well, it's spinning there and
watching for more "work" to come in, then doing that work and pushing
the results back upstream.

This is complicated and horrible. It's faster, but messy. It also
parallelized the fetcher, but not the crawler! What if we want everyone
to be able to crawl at once in one python program? We already had to
rewrite everything to make the fetcher parallel, we don't want to have
to do it all again. There's an example on github but it's huge.

> I hate this

Let's make it better

# The New Way

`@asyncio` and `yield`. The code is in the slides, and it is beautiful.
You don't rewrite your code entirely, you just use the Tulip format to
tweak the way your data is being passed around.

Okay, so this is cool but it's not actually async. So how do we actually
crawl in parallel? To fully parallelize, we just need a few more tweaks.
When you call a coroutine, you're actually just getting a promise
("future") back. If you yield from the future, you'll get back the
result. But if you DON'T yield, your future sticks around. So let's
create a bunch of them and _Fan Out_.

We now have a whole batch of futures, so we iterate over them _in the
order they finish_ and get all our results. That way, if something takes
forever to return we'll just skip that future until it does. As they
finish up, we fan em back in.

That's it! Small, fast, very small delta from our original stupid code.

# It's Everywhere

Once you start thinking about this pattern, you see it everywhere.

- SQL joins are fan-out, SQL grouping is fan-in!

- MapReduce == FanoutFanin

- Histograms: you have a ton of things, so you fan em all out into their
  components, then fan them back in to the buckets

- etc

# Links

Lots of links on the slides. Some good libraries, some good talks.

