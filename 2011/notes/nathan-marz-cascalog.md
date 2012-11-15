# "Cascalog", Nathan Marz #
[Slides](../2011-slides/nathan-marz-cascalog.pdf)
[Code](https://github.com/nathanmarz/cascalog-conj)

## Let's do some analysis ##
   * On the tweets during the tunisia uprising

## What is Cascalog? ##
   * Abstraction on top of Map / Reduce
   * ...

## What is Hadoop MapReduce? ##
   * High latency batch processing
   * Massive scale (petabytes)
      * Can scale horizontally across as many nodes as you need
   * Fault-tolerant

## Why Cascalog? ##
   * Hadoop MapReduce can become quite unwieldy as your logic requirements grow
   * Cascalog provides help with
      * Abstraction
      * Composition

## Cascalog Basics ##
   * The 'age' dataset
      * first field name
      * second field age
   * Query
      * `(?<- (stdout) [?person] (age ?person ?age) (< ?age 30))`
      * `(?<- ...)` define and execute query
      * `(stdout)` where to put the results
      * `[?person]` output variables
      * rest - predicates constraining the output variables

## Predicates ##
   * Example:
      * `(* 2 ?x :> ?z)`
      * ...
      * `?x` input fields
      * `?z` output fields
      * ...
   * It's wrong to think of predicates as functions
   * Instead they define constraints on fields
   * Four kinds:
      * functions
         * operate on a single tuple
      * filters
         * define constraint on set of input e.g., >, <
      * aggregators
         * operates on multiple tuples, e.g., counting or summing
      * generators
         * finite sources of tuples
         * e.g.,
            * vector
            * 3 Gb dataset
            * database table

## Join Example ##
   * `(def follows [["alice" "david"] ["alice" "bob"] ["alice" "emily"] ["bob" "david"] ...])`
   * ...
   * Joins are implicit

## Demo ##

## Data Model ##
   * Stored as data on nodes or edges between nodes
      * there are two types of node
         * reactors are the cause of reactions
         * reactions are events representing something that has happened
      * nodes can have meta data called properties

## Composability ##
   * 
```
(?<- (stdout) [?avg-age]
  (age _ ?age)
  ...
```
   * expands into
   * ...
   * The result is a "predicate macro"
