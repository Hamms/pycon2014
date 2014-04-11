[Castle Anthrax: Dungeon Generation Techniques](https://us.pycon.org/2014/schedule/presentation/146/)

The slides contain examples of the (pretty damn basic) data structures
and algorithms that are being used here. Nested lists, lists with row
basic ordering, 

# Maze Generation

Super simple: throw the cells in a stack, grab all the "unvisited"
neighbors, and remove a random wall. Analogous to depth-first search.

`Prim's Algorithm` is a more interesting one; analogous to A\*.

So these two algorithms will produce two very different "styles" of
maze. The DFS gives us very long, twisty corridors; Prim's is shorter
and more blocky. 

# Feature Placement

However, we don't just want a maze, we want a dungeon with rooms! A
simple approach would be to just drop a room down and then look for a
place we can put another, but we can be far more clever than that.

So let's make a binary tree! Create a space partition and recurse
semi-randomly until we have as many leaf nodes as we want rooms. Then we
can connect our rooms with any of the various binary-tree traversal
methods.

Some other things:

- *Cellular Automata*: something like Conway's game of life can let us
  generate caves

- *Poisson Disks* can be used to place things like enemeis or treasures.
  In graphics, these are used to do things like place vegetation.

- *Perlin Noise* or simplex noise generates "cloudy" textures. So you
  can do things like create pits! With bridges!

# Constraint Solving

A constraint solving problem is where you have a bunch of variables
whose values are within some range (either continuous or discrete).
Let's just talk about finite domains cause that makes more sense for
games.

So what's involved in a contraint solver? Well, a variable (or more than
one), with a domain of values, and a constraint that takes some number
of variables and provides a constraint.

For example: the eight queens problem.

In dungeon design, a simple example is that we want the end boss to be
close to the exit. Or we want there to be health potions relatively
close to monster encounters.

Constraint solving is all about narrowing down the search space. As soon
as you place a queen, you no longer need to consider any of the squares
that are threatened by that queen. We go through and narrow down our
search space until each variable has a unique value.

You can easily implement a rather naive version of this, and the slides
show this off.

# Conclusion and Q&A

The slides contain some great resource links, including one for
*PYANGBAND*. 

If you're building something stylistically similar to existing content,
markov chains are also an option!

most of these algorithms are n-dimensional

Creating "ruins" is a process of generating something and then
destroying it. A combination of poisson disks and perlin noise can be
very effective for this.

