# "Learning Clojure - Next Steps", Stuart Sierra #
[Slides](../slides/stuart-sierra-clojure-next-steps.pdf)

## Already? ##
   * 4Clojure - clojure exercises
   * Books - Programming Clojure, Joy of Clojure, Clojure in Action, 
   * IRC channel
   * StackOverflow

## What Next? ##
   * Reader and writer
      * Writer functions
         * `(println ...)` - human readable
         * `(prn ...)` - machine readable, when read back, will be equal, 
            * `*print-readably*`
            * `*print-dup*` guarantees this
            * `*read-eval*` whether or not should eval after reading
         * `(print-method ...)` - multimethod dispatching on type
         * `(print-dup ...)` - multimethod dispatching on type
         * `#=()` - backdoor into the reader, useful when working with `(print-dup ...)`
      * Resources - additional uncompiled files accompanying an artifact
         * `(io/resource ...)` - read text from resource file
         * `PushbackReader` needed by clojures reader
         * `(read ...)`
         * Ability to separare read and eval programmatically
      * Clojure vs. JSON
      * Ideas
         * Custom readers, different defaults
            * Reader macros!
            * Reader printer for other formats
   * Interfaces
      * `(print-tree ...)` (custom to Stuart) - prints `(inheritance-tree (class x))` nicely
      * `(assoc ...)` - references RT, clojure run time `(rassoc ...)`, in turn references Associative.assoc, implements interfaces
      * Custom collections
         * May be able to get performance gains by writing primitive specific collections where possible
         * Identify hotspots via profiling
   * Raw Concurrency
      * Executors
         * All clojure functions are callable
      * `AtomicReference` - one of the Atomic types
         * Clojure's atom based off this
      * `AtomicLong` - atomically updateable integer value
         * May compile down to machine instructions, therefore more performant
      * `CountDownLatch`
         * Pause threads and have them wait on something else
      * More stuff:
         * `CyclicBarrier`
         * `Semaphore`
         * `Exchanger`
      * Concurrent Collections - thread safe, not governed by single exclusion lock
         * e.g., 
            * `ConcurrentHashMap`
            * `ConcurrentLinkedQueue`
            * `ConcurrentSkipListMap`
            * `ConcurrentSkipListSet`
         * Shared cache?
      * `BlockingQueues` - data structures for synchronisation
         * `SynchronousQueue`
         * `LinkedBlockingQueue`
         * `LinkedBlockingQueue`
         * `PriorityBlockingQueue` etc.
      * Plain old locking
         * `(locking object)` equivalent to synchronised `(object) { }`
         * `ReadWriteLock`
         * `ReentrantLock`
      * Volatile 
         * New value can't depend on old value - doesn't guarantee anything
         * Write from one thread, value immediately visible on every other thread
         * Does not guarantee atomicity of update operations
      * Unsynchonised - no guarantees, the default in Java
      * Cljque - new concurrency primitive, notifier, (not ready for adoption!)
      * Ideas
         * Explore Ref history - performance implications if multiple threads reading and writing same ref
         * Partial locks - locking part of a data structure so that it doesn't all block
         * Distributed locks / transactions - unsolved problem
         * Eventual consistency
         * Connect to other transactions systems, databases, Java EE
   * Explore
      * `clojure.test.generative`
         * specify inputs to a function
         * randomly generate inputs using that spec
         * assert general rules about the output - universal properties, invariants
      * `clojure.core.logic`
         * variant of prolog, 
         * logic programming - write program as a series of facts and ask questions of whether something is true
   * The JVM and Beyond
      * Class loaders
         * compile source code into bytecode
         * load bytecode into JVM
         * control visibility of classes inside the JVM
      * ASM / bytecode
         * Less than 200 op codes in bytecode, many redundant
         * Not too tricky to learn
      * JNI / JNA
         * Native access
         * JNA easier to use, JNI requires C
      * JSVC
         * Apache project
         * Java service container
         * Allows Java programs to interoperate properly with UNIX environments
            * process management, forking, joining etc.
   * Make Stuff!
      * Make libraries not frameworks!


