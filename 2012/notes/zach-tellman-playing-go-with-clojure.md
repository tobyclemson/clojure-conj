# "Playing Go with Clojure", Zach Tellman #

## Rules of Go ##
* See [Go on Wikipedia](http://en.wikipedia.org/wiki/Go_(game))

## Shall we play a game? ##
* Let's write a program that plays Go

## My Qualifications ##
* I'm a mediocre Go player
* I think this stuff is pretty cool
* I've written performance-oriented Clojure before

## The Game Tree ##
* Current state is root node
* Direct children are possible next states
* Continues down to leaves which represent the end of the game
* Search for a path through the tree
* In a cooperative or single-player game, we only need to search for
victory
* ...

## Minimax ##

* Assign a value to each leaf node
* Assign the parent the maximal child value if it's our turn or the
* Minimal child value if it's our opponent's turn
* Ascend one level, and repeat
* Plays a perfect game
* Requires traversing the entire tree
* There are ~9 ...
* Construct a shallow game tree
* Assign each leaf node a value based on our best guess at the outcome
* Apply minimax to these values
* Can't do this with Go as it is too expensive
* Get a heuristic view by keeping a shallow game tree

## The trouble with heuristics ##

* Difficult to quantify
* Depth vs. quality
* Understanding a function vs. understanding its repeated, recursive application

## The trouble with go ##

* Lots of breadth
* Lots of depth

## Historical approaches ##

* Programmers who are professional-level players
* Shallow and narrow searches, heavy evaluation functions

## Monte carlo simulation ##

* Imagine quarter circle inside a square
* `(defn inside-circle? [x y]
    (>= 1 (+ (* x x) (* y y))))`
* `(defn sample ...)`

## Monte carlo evaluation ##

* The strength of a position is how often one side wins,
* Given repeated, naive playouts by both sides
* Possible playouts vs. plausible playouts
* Each new playout gives us additional information about what is
plausible

## Multi armed bandit ##

* Multiple levers to pull, each with an unknown expected reward
* Exploitation vs. exploration
* If the search space is stable over time, we expect to converge on a
solution

## Monte carlo tree search ##

* selection -> expansion -> simulation -> backpropagation -> repeat x
times

## Simulating go with clojure ##

* Select a move
* Check for suicide
* Make move
* Check for capture
* Repeat

## Incremental state ##

* Group, pointers to owner of group
* Pseudo-liberty, surrounded means zero liberties and zero pseudo-liberties
* We keep track of the pseudo-liberties ...

## A little arithmetic ##

* 1 second / 10,000 games per second / 100 moves per game = 1
microsecond to make a move...

## A quick descent into insanity, no performance ##

* not your day job
* not latency bound
* faster is smarter
* diminishing returns not within reach

## Mutable state ##

* so, we have to use mutable state
* for experts only
* if a value is only used on a single thread, it can be unsynchronised
* otherwise volatile
* ...

* `(deftype Mutable [^:unsynchronized-mutable ^long counter]
    IMutable
    (get-counter [_] counter)
    (set-counter [_ val] ...))`

## Criterium ##

* One of the many great libraries from Hugo Duncan
* Use it at the REPL and in your tests
* Tends to exaggerate cache coherency
* Minimum resolution appears to be ~15 nanoseconds

## Bottom-up performance ##

* Measure each piece of your code
* Measure them when used together
* Build an intuition for how long something should take, and
  investigate when you're wrong

## Indirection ##

* Methods dispatch to different things in different places
  * = -> == or identical?
  * count -> Array/getLength
* Primitive maths

## Plumbing the depths of performance, no insanity ##

* Simulating C-style structs with ByteBuffers
* Mimicking C compiler offset calculation with local analysis
* Creating a bridge to heterogenous computing
