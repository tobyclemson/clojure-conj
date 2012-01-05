# "Striving to Make Things Simple and Fast", Phil Bagwell #
[Slides](../2011-slides/phil-bagwell-simple-and-fast.ppt)
[RM Trees Paper](../2011-misc/RMTrees.pdf)

## Introduction ##
   * [Asked how many people in the audience had Clojure in production] (not many)
   * [Asked how many people wanted to have Clojure in production] (many)
   * Engineers tend to view the world as a series of engineering problems
   * So, look at the organisation as an engineering problem in terms of convincing managers, colleagues to adopt Clojure

## Parallel Collections ##
   * Automatic multi-threading of comprehensions
   * Comprehension is applying a function to a collection
   * Simple to change from sequential to parallel
   * Split work by number of processors
   * Each thread has a work queue that is split exponentially, largest on top of queue
   * Granularity balance against scheduling overhead
   * On completion threads 'work steal' from othegramr threads
   * Easy to program
   * Excellent speed ups in multi core systems
   * Good load balancing
   * Not universal fix to all concurrency problems

## Non Blocking Resizable Concurrent Hash Tries ##
   * Caches, dictionaries, time varying analytics
   * Scale well in multi core
   * Allow snap shot
   * Lock free hash map

## Non Blocking Snapshot ##
   * Baseball problem
   * Can take non blocking snapshot of cht in small constant time
   * Changes to sn do not change cht
   * ...
   * Example
      * People in a room, by the time you have finished counting, people have left and entered
      * Solution, take a snapshot, like a photograph, can carry on working without worrying about external changes

## Vectors - Today's Problem ##
   * Two vectors, want to concatenate them
      * `concat(A, B)` -> linear time in B
      * `mid(A, 30, 50)` ?
      * `left(A, 10)` ?
      * `right(A, 50)` ?
      * `concat(right(concat(A, left(B, 10)), 5), B)`
   * And parallel comprehensions
      * ...

## Immutable Vectors ##
   * ...

## Vectors ##
   * Mutate:
      * Update value immutably
      * Copy all nodes on path to updated value

## ... ##

## Back to Array Concatenation ##
   * Ropes?
      * determine which side of the tree to traverse down based on required index
      * unfortunately, tree gets deeper and deeper over consecutive rope operations
   * B-Trees?
      * Few levels like vectors
      * Updates, iterations, etc. all good
      * Concatenation cheap ~= update
      * Simple to balance
      * But: Radix index search impossible
      * Idea: Add item counts at the level and use ...
   * B-Trees + Item Counts?
      * Better
      * Idea: Make all node m or m-1 in size to get near radix search
      * ...
   * RRB-Tree Attempt 1
      * Index speed constant 60% slower than standard vector
      * Low memory overhead (1/m)
      * Updates, iterations, etc. all good
      * But: Costly to balance
      * 3-4 RRB Trees
         * Follow edges
         * ..
      * Concatenation cost > 30x update
      * Idea: Constrain overall extra search steps not node size
   * RRB-Tree Attempt 2
      * Principle: look for first less than m-1 and combine with enough following to reduce node count by one
      * Index speed 60-70% slower than standard vector
      * Memory overhead still good
      * Updates, iterations all good
      * Concatenation costs 2 to 6x update, very good
      * Standard until concat or splits used
      * Negligible degradations with many splits of concats
   * RBB-Tree Left/Right Slice
      * Follow slice path
      * Rewrite path with left or right removed
      * Only rebalance on concatenation


