# "Keynote: Areas of Interest for Clojure's Core", Rich Hickey #

## Introduction ##
   * This is not a roadmap!
      * This stuff may never make it into Clojure
      * Needs design time and effort
      * It's a bit half baked

## Leaner ##
   * Memory footprint
   * Startup time
   * Filesystem footprint
   * Why?
      * Delivering libraries written in Clojure to non-Clojure
      * Smaller targets, e.g., Android
   * Move ASM out
      * Currently bundled in
      * Dynamic compilation only happens in the REPL
      * Unless your program calls (eval ...), no dynamic compilation happens in clojure.core
      * Adding rules to a running system is probably rare
   * Dev-less builds
      * No metadata, shaking etc.
         * Need multiple build targets, currently have just one
      * Debug builds
         * Could also go the other way and have bigger builds including more decoration of code
   * Lisps traditionally have very good tool support

## Unification with ClojureScript ##
   * ClojureScript is Clojure on a different host
   * Shared source libraries
   * Conditional compilation
      * Also needed by Clojure CLR
   * Unifying on CLJS analysis rep for tooling
      * Potential for common tooling
   * It has never been a goal of Clojure to be able to take an entire app and move it between hosts
      * That doesn't give you very much
      * However it does add lots of extra layers of abstraction over the hosts
   * It would be nice to have a conditional knob to be able to choose what is compiled as ClojureScript and what is compiled as Clojure
   * "Looks like a lot for a human but it's nothing for a machine",
   comparing the ASTs for CLJS to those for Clojure

## Prepping for Clojure in Clojure (CinC) ##
   * Move protocols down to the 'bottom'
      * directly emitted by compiler
         * currently require quite a lot of Clojure to be functional
         * high level macros
      * value seen in ClojureScript
         * experimented with having (deftype ...), (defprotocol... ) etc. deeper down in ClojureScript
         * libraries and abstractions thus built on top of them
         * made it a pleasure to implement them
   * "Refactoring, I hate that word!"
   * Organising CLJS compiler for multiple targets?
invokedynamic
   * What it is
      * Code-gen and class-free call sites
         * Class is pretty big and carries lots of baggage, when each function requires a class, that gets expensive

      * Access to safe point 'magic'
         * A safe point is a magic implementation detail used during bytecode loading (?)

         * Helps you to build tools to do dispatch without writing any extra code
   * For Clojure
      * protocol / keyword call sites
         * polymorphic call site dispatch
      * fast + dynamic vars
         * var is an indirection and volatile
         * difficult to inline them when they become hot spots
      * reflection-free interop
         * no need for type hints
         * one time only reflection, builds typed call sites
         * not in deep need but would be nice as a backup
   * Tradeoffs
      * Performance
         * should improve with more recent builds of Java 7
      * Java 7 and above only, thus only in addition to what is already being done

## Leveraging Logic ##
   * code -> analysis -> `core.logic`
      * don't settle for 'type checking'
      * queryable programs
   * predicate dispatch
      * don't settle for 'pattern matching'
         * "I don't like pattern matching"
            * it's closed
            * it's order dependant
         * This means new patterns can't be added as the order of patterns is important
         * This goes away with predicate dispatch
      * is `core.logic` fast enough for this?
         * precompile dispatch trees

## Parallelism ##
   * Good concurrency support in place
   * Is fork/join framework the right thing for mixed (compute + I/O) models?
   * Is it the right thing for balanced compute models?
      * We can partition our system into I/O and compute on a case by case basis
      * However this isn't possible in the general case
      * Ideal when branching points lead to varying amounts of work
   * Parallel algorithms, not collections
      * "We don't attach our functions to our data, we apply our functions to our data"
      * however, collections must have good 'shape'
      * seqs do not
      * we have parallel map and parallel reduce, would like to extend this to other operations

## Transients and Beyond ##
   * Transients do too much
      * Persistent symbiosis and editing
      * and policy
   * And too little
      * Users must use linearly
   * Better to have a construct for this
      * Need to make sure the user doesn't have to be burdened with what they're doing
   * Transient based model
      * Make into a transient in new memory (possible in constant time)
      * Apply procedures (possibly many) resulting in transients
      * Then make result persistent
   * What about those transient -> transient procedures?
      * Might modify their arguments
      * Isn't this just icky mutable side effects?

## Procedures ##
   * Function of transient to transient
   * Like pure function, can't affect the world nor be affected by it
   * Only used in a context where transient cannot leak
   * Can always be sandwiched in value -> transient and transient -> value functions and become 'pure'

## Pods ##
   * Split out policy from data structures
   * New policy:
      * value in, value out
   * Process goes through the pod
   * Coherent process creates next value
   * Multiple options
      * single threaded
      * multi threaded access via mutex
   * Work with transients
      * Just take policy out
      * Persistent map in, transient map inside, persistent map out
   * Don't require persistent <-> transient!
      * Can work with immutable <-> mutable
      * String in, StringBuilder inside, String out
      * Provide a recipe for using ordinary Java stuff in a managed model
   * The first construct that can apply to ordinary Java stuff
   * How do they look?
      * Wrap a pod around a persistent data structure: `(pod [])`
      * Send operations in: `(>> ...)`
      * System is extensible

## Pod Power ##
   * Pods allow process to extend across multiple functions and pods
   * Multi-threaded pods allow process to extend across cores
      * Pods can ensure lock acquisition problem
      * Pods can't fix the lock composition problem
         * but this can be detected
   * Pod based clone: `@(pod x)`
   * Pod peeking: `(<< count some-pod)`
   * Should internal pod representation be a function of value type?
   * Or should we allow user-specified pod contents?
   * Can pods be revisited after producing a value?
      * Possible but may not be desirable
   * Pod groups, sentry sharing
   * Multithreaded pod API:
      * `(in-pods [a b c] ...)`

## Accumulators ##
   * Pods...do too much?
   * Most use is building / birthing
   * Maybe all we need is conj! / append
      * making details internal
   * Same front end for accumulators and queues and ...
      * hmm

## Extensible Reader ##
   * Why?
      * Clojure data is a great serialisation format
      * More types
      * "XML has X and we don't have X"
      * What do we do right now? All kinds of things to extend
      * Fewer types means less self-describing
         * forces us to use existing data types to represent other types
         * XML allows data types to be introduced
   * But
      * Less consensus on representations
      * Avoid wheel rebuilding
   * Premise
      * Meet at semantics and print / read representation
      * Plug in desired programmatic type
   * How
      * Tags
      * On other readables
   * e.g., 
      * `#instant "1985-04-12T23:20:50.52z"`
      * `#ints [0 1 2 3 5 7]`
      * `#my.ns/foo {:bar 123 :baz [5 6 7]}`

## Questions ##
   * Have you looked at YAML's tag format? It's very similar and might help with implementation ideas...
      * Yeah, I'm not claiming originality, I ripped it off from Erlang
   * '`*print-dup*`' spits out classes and '`#=`' etc., how is this different?
      * It's about semantic meaning of data, not about specific implementation
      * '`*print-dup*`' will distinguish '`HashMap`' from '`ArrayMap`' whether you like it or not
   * Where does agreement happen about what '`#instant "foo"`' will rehydrate to?
      * No agreement
      * Can't dictate data structures
   * Have you looked at openmath?
      * Might be worth a look
   * Can you elaborate on querying programs?
      * Simple things like how often do we call this function?
      * How deeply nested are calls function?
      * Have we ever called this will an open file in hand?
      * Program analysis stuff
      * Cross cutting concerns
   * Conditional computation for targetting different platofrms - what about specifying an interface that implementations must implement?
      * Don't like that at all, you're talking about reifying environments
   * Pods solve generating a value, how about iterating over a collection using mutability as a performance optimisation?
      * To do this you have to hand off the work of doing a job to something that knows the implementation details of the type being manipulated
      * Haskell does some stuff with stream fusion which is a good example of the type system helping 
   * Platform power, access to safe points, devless builds: what is the most predominant platform power?
      * we have great platform power
      * need to make things slightly more efficient whilst keeping all platform features
   * You talked last year about the issue of resource management in the presence of laziness. Are you any closer to solving the issue?
      * lazy evaluation might e.g., hold onto resources until evaluation reifies and allows resources to release
      * problem is harder than I thought

