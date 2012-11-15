# "Extreme Cleverness: Functional Data Structures in Scala", Daniel Spiewak #
[Slides](../2011-slides/daniel-spiewak-extreme-cleverness.pdf)
[Code](http://github.com/djspiewak/extreme-cleverness)

## Background ##
   * The title says 'Scala' but most of this is equally applicable to
   any functional language

## Agenda ##
   * Functional data structures
   * Implementations
      * Sequential
         * Preserves insertion order, fast access to head or tail, not to the middle so not so good for random access
      * Associative
         * Don't preserve insertion order but provide good random access
   * Modern computer architecture
      * How this affects the design of our data structures

## Functional Data Structure ##
   * Immutable, immutable, immutable!
      * Not that difficult to create, just copy on write
      * However this has terrible performance
   * What we want:
      * Comparable asymptotic performance
      * Non-degraded versions
         * full persistence

## Sequential Data Structures ##

### Singly Linked List ###
   * Compexity:
      * first : O(1)
      * everything else : O(n)
   * Anatomy:
      * a list is either:
         * a "cons" cell with a value and a tail
         * an empty list, called nil
      * these are the only cases
   * Structural sharing
      * `val foo = a :: b :: c :: d :: nil`
      * `val bar = h ... b`
      * `val baz = m :: n ... a`
      * `val raz = q :: r ... n`
      * find that bar shares some of foos structure etc.
   * The goal is to minimise the amount of copying and maximise the amount of sharing
   * Once achieved, we obtain powerful immutable data structures with
   good performance characterstics

### Motivation ###
   * We want a functional queue
   * Linked list is obvious
      * prepend and last are opposing
      * one will be O(1), the other O(n)
   * Can we have our cake and eat it too?
   * Bankers queue attempts to do this

### Bankers Queue ###
   * Complexity:
      * append, last, prepend : O(1)
      * others : O(n)
   * Anatomy
      * Naive persistent queue
      * Two lazy singly-linked lists
         * front list (for dequeue)
         * rear list (for enqueue)
      * Periodically reverse rear into the front
      * Lazy amortisation

### Amortisation ###
   * Most operations are legitimately fast
      * Few operations are very slow
   * Laziness distributes the work
   * Net result: constant factor degradation
      * Translation: the net average is fast
   * Also works without laziness!

### 2-3 Finger Tree ###
   * Complexity:
      * append, first, last, prepend : O(1)
      * insert, nth : O(log n)
      * rest : O(n)
   * Anatomy:
      * Ideal persistent deque
      * Digits of length 1, 2, 3 or 4
         * Head and tail
      * Branching factor of 2 or 3
      * Recursive tree body
         * The need to decend deep into the tree reduces exponentially so we have amortised time
   * Unfortunately this is really slow in practice

## Associative Data Structures ##

### The Red-Black Tree ###
   * Complexity:
      * get, insert, update: O(log n)
      * intersect, union: O(n)
   * Anatomy:
      * Balanced binary search tree
      * Invariants
         * Every path from root to a leaf contains the same number of black nodes
         * No red node has a red parent
      * Need to rebalance after any "update"

## A Little of Both? ##

### Bitmapped Vector Trie ###
   * Known in Clojure as...the vector
   * Complexity:
      * append, first, last, nth, update : O(1)
      * concat, insert, prepend : O(n)
      * almost...
         * actually O(log_32 n) 
         * which is approximately O(1) for any data structure which can fit in memory
   * Anatomy
      * Start with an array with max length 32
         * copy on write
      * Array of arrays, max length 32
         * Array of array of arrays, max length 32
            * etc.
      * Maximum depth is 7!
   * The performance is ridiculous! Crazy fast!

## Modern Architectures ##
   * Locality of reference
   * Caching
      * Bite-sized data chunks
   * JVM considerations
      * Heap locality
      * For example
         * in theory a linked list should not have good locality at all
         * in practice we do get locality because the JVM is smart
         enough to know you're using a linked list so it preserves
         locality of entries as much as possible
      * This is the reason the 2-3 finger tree is NOT fast
         * JVM can't help you as you have pointers to pointers to
         pointers ...

## References ##
   * Okasaki: "Purely Functional Dta Structures"
   * Okasaki: "Red-Black Trees in a Functional Setting"
   * Hinz & Peterson: "Finger Trees: A Simple General Purpose Data Structure"
