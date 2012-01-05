# "Concurrent Stream Processing", David McNeil #
[Slides](../2011-slides/david-mcneil-concurrent-stream-processing.pdf)

## Background ##
   * Been building a database query translation and federation product
   * Databases -> Concurrent stream processing -> result set

## Needed stream operations ##
   * ...

## Other Requirements ##
   * Efficient
      * Parallel execution
      * Non blocking on source IO
   * Robust
      * Exception Handling
      * ...
   * Manageable
      * ...

## Shoulders of Giants ##
   * Oracle, Sun etc.

## UNIX ##
   * Pipes:
      * Processes:
         * concurrent
         * separate address spaces
         * multi-threaded
         * stdin, stdout, stderr
      * Pipes
         * asynchronous
         * buffered
         * EOF
      * Operators
         * standard library
         * extensible
      * All run in an execution environment that understands how they
      fit together

## In Clojure ##
   * Pipes and Nodes
      * Clojure library
      * What syntax would we use to achieve this?
      * Just use s-exps to represent the process tree
   * From the bottom up, how would we build this?
      * Pieces
         * Pipe writers
         * Pipe receivers
         * Pipe callbacks
         * Pipe protocol - encapsulates these behaviours
         * Pipe multiplexer - join
         * Pipe tee - fork
         * Processing nodes
            * Input pipe
            * Output pipe
            * Processing node
               * state
               * concurrency
               * in/out/function
         * Chunks in pipes
         * Processing trees
            * fire lots of threads at each of these parts
      * Externally:
         * Data sources
            * database queries, files, whatever
         * Result
            * output at the end of the pipe tree
      * Nodes:
         * Push and pull between producers and consumers
      * Efficient use of worker threads?
   * Java fork/Join - fork join pool
   * Higher level
      * Processes
         * consists of many pipes and nodes
      * Memory
         * Pipes go onto the heap when dead
         * How do we handle low heap space?
         * Swap in buffered pipes
      * Cancellations / Timeouts
         * Nodes can be shutdown
   * Stream expressions
      * Tree of pipes ending in clojure expressions
      * How to compile?
      * Work from bottom up
   * Stream operators
      * Mirror clojure sequence operations
      * Can take parts of streams
      * Let operators allow working with results of streams in other streams
   * Compiling vs. Evaluating
      * Stream expression compiler separate from stream expression evaluator
      * Compiling
         * zipper walks the tree
         * compile macro compiles each piece

## DSL Approach ##
   * s-exps
      * produced via Clojure mechanisms
      * passed around as data
   * unqualified symbols from operators
   * tree of know operators
      * avoid general code walking
      * user macros expand to know operators
   * multiple operator implementations
      * some invoked via clojure...
      * ...
   * expressions do no eval to their final value

## Code Generation ##
   * Effectively writing a database
   * Application generates a program to process each query

## Tuple Processing Expressions ##
   * Working on defining higher level tuple operations

## Distributable Stream Processing ##
   * Break process tree into parts
   * Evaluate each in a distributed manner

