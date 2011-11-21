# "From Linear To Incremental", Christophe Grand #
[Slides](../2011-slides/christophe-grand-from-linear-to-incremental.pdf)

## Background ##
   * In the beginning there was frustration
   * Why do I need to reparse a whole file when I make a minor edit?
   * Changing one symbol doesn't change any structure
   * ...

## Consequences ##
   * Simple edits should be incremental
   * O(log n) rebuilding the parent index
   * Recom...

## Incremental Parsing ##
   * Definition:
      * Recompute the whole parse-tree at a fraction of the cose after an edit
   * Overloaded term:
      * Restartable
      * Lazy restartable (Yi, Haskell editor)

## What's a parser? ##
   * Consumes a string, returns a tree
   * A reduction:
      * `(get-tree (reduce parse-step init input))`
   * Many programs can be coerced into such a form

## It can't be that hard ##
   * Just another reduce
      * The proglem isn't specific to parsing
   * Solve the general case
      * Famous last words
   * `(reduce parse-step init input*)` knowing `(reduce parse-step init input)` and diff vetween `input` and `input*`

## Reduce considered slightly harmful ##
   * Unconstrained fn = sequential computation
   * Detrimental to parallelism and incrementalism too
   * Incrementalism is parallelism with your former self

## I <3 Associativity ##
   * Can let you change tree and balance it
      * `(= (f (f a b) c) f a (f b c))`
   * Sad fact: most functions aren't associative
      * parse-step not associative
         * state * token -> state
      * associative functions are A* x A*
   * Have
      * `(reduce f init [a b c d])`
   * Compose together:
      * `#(f % a) #(f % b) #(f % c) #(f % d)`
   * `(comp ...)` is associative
   * Incremental yet?
      * Yes, but composition is incremental, not the actual computation
   * init is constant, incrementalism presupposes things don't change that much
   * Memoise nodes, though not the map and compose
   * Better, but:
      * some computation is skipped ...
      * composition tree + memoized ...
      * much ado about nothing!

## Refining memoization ##
   * Once an item differs, the output differs
   * Subsequent memoized results aren't used
   * How to leverage past computations?
   * Need to look at the state passed around - function specific

## What's the function? ##
   * A parser step fn!
   * Minimally fancy algorithm
   * LR + contextual tokenizer

## LR ##
   * A pushdown automaton
      * One finite state machine 
      * ...
   * Step:
      * current state change:
         * push / peek / pop on stacks
      * deep stack items are ignored
         * note even read stack lengths are ignored too
      * Depends only on:
         * ...
   * What's in a stack?
      * stratified by construction
         * local importance near top
         * distant/ global imporance near cottom
   * Concluson
      * steps are not influenced that much by distant changes
         * As long as current state and enough stack
      * top items don't change true from composition too
         * skipping several steps at once

## Stack Transplantation ##
   * First call: in (abcdef)  -> out (zcdef)
   * Next call: new in (abcghij) + previous out (zcdef) -> new out (zcghij)

## Differential memoisation ##
   * Like memoization but works for input resembling known inputs
   * Tweak memoised output to match new input
   * When input too different, call the actual function

## Transplantation ##
   * Best case: everything is reused
      * runs in logarithmic time
      * incremental, at last!
   * Worst case: restartable
   * Two functions are needed:
      * One to approximate dependencies between output and input
      * One to quickly compute a new output based on a new input matching dependencies of a known [in out] pair
   * Totally dependent on the algorithm
   * So dependent on the algorithm that:
      * ...

## Dependencies ##
   * I use side-effects
      * tracing operations on stacks
      * easy, fast, expedient
      * ...

## Inside the step function ##
   * Stacks are made mutable
      * Reduces object churn
   * Processes a chunk of text
      * Reduces memory overhead
      * Reduces <<context>> switches (persistant / mutable)

## The buffer ##
   * Parsley API
      * `(parser options & grammar)`
      * `(incremental-buffer parser)`
      * `(edit buffer offset length s) ;; composition`
      * `(parse-tree buffer) ;; actual composition`

## Composition tree ##
   * Reasonably balanced: 2-3 tree
      * Leaves are partial functions
      * Internal nodes are compositions
      * All nodes know their length in order to find where to perform edits
   * A finger-tree may fit but:
      * The 2-3 tree was easier
      * No need for privileged access to ends
   * ...

...

## Demo ##

## What's next? ##
   * Refine dependencies computation
      * Think hard how to mechanise that
   * Try to incrementalise other parsing techniques (namely GLR)
   * Minor but practical feature: bridge with the Regex DSL
   * Make the emperative code less brutal
   * More caching strategies
   * 
