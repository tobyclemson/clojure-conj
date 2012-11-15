# "The Macronomicon", Michael Fogus #
[Slides](../2011-slides/fogus-macronomicon.pdf)

## Programs Writing Programs ##
   * Code generation
      * XDoclet
      * XText
      * Lombock
      * Velocity, Erb
      * MDA
      * Rails
      * Hacks
   * C
      * A long time ago, C had an interesting property: 
         * you could define macros that would replace any text in your program at compile time (preprocessor directives)
         * this caused problems
         * instead it evolved into a more constrained expression macro language
   * C++
      * Template metaprogramming
         * e.g., factorial
         * Bohm and Jacopini
         * values, functions, branching, recursion -> Turing completeness!
   * OCaml
      * From this: `List.map (fun x -> x+1) [1; 2; 3;]`
      * To: abstract syntax tree
      * The expander: `<:expr< ... >>`
   * Lisp
      * Lisp macros!
      * Use cases:
         * creating binding forms
         * creating control flow
         * icing

## History ##
   * Lisp:
      * The original lisp eval...
      * AIM-57
         * Macro definitions in lisp
         * Timothy Harp
      * Lightweight fn / blocks
         * control flow
         * bindings
         * e.g., Ruby
   * Scala
      * Baysick - Scala DSL for Basic :)
   * Mapping Dilemma
      * One of the issues here is actually encapsulation: without macros the ability to create abstractions is limited by the degree to which underlying language constructs peek through the abstraction barrier
   * Use cases:
      * ...
      * "All legitimate uses of macros are legitimate" - Yogi Berra
      * Let's add:
         * Abstraction
         * Transformation (Houdini, biolerplate)
         * Optimisation
         * True power awesomeness!
   * What do you want?
      * A way to define local bindings
      * Properly scoped
   * Do you need a macro?
      * e.g., function memoiser...didn't *really* need a macro so didn't use one
   * What is it really?
   * Just start typing and it'll all work out fine!

## Hygiene ##
   * An hygeinic macro is one where the meanings of symbols that aren't parameters to the macro are ...
   * Degenerative case 1
      * A macro that returns true when the value it is passed is true
      * Hygeinic as clean vs. unhygeinic as dirty or rotten
   * Degenerative case 2
      * `(defmaco awhen ...)`
      * Hygeinic as sterile vs. Unhygeinic as getting things done

## Use and Abuse of Macros ##
   * Don't want to talk about DSLs
   * Instead let's talk about MSLs: mood specific languages
   * e.g., 
      * Trammel
      * Step 0: What did I want?
         * Goals
            * New `:pre`/`:post` syntax
            * Decomplected contracts
            * Invariants
            * ...
      * Step 1: Do I need a macro?
         * Yes
         * Second class forms
         * Macros are first class at making second-class forms
         * Macros: why wait for Rich?!
            * He gave me the power and I'm going to abuse it...er I mean use it
      * Trammel is...
         * a new `:pre`/`:post` syntax
         * decomplected contracts
            * define a function, later on apply a contract to it
         * record invariants
         * better error reporting

## Piecewise Transformation ##
   * Disassemble a data structure that comes in
   * Incrementally manipulate it in pieces
   * Build back up into the thing the macro is producing
   * e.g.,
      * `(as-futures ...)`
      * actions distributed over a number of futures
   * The nice thing is during the piecewise transformation you can attach functions that validate each piece and give more refined error handling

## What Lies Beneath... ##
   * Build your macros on a solid foundation
   * Primacy of Semantics
   * A contract:
      * A function that takes a function and a number of arguments
      * Applies some pre and post conditions and then delegates to the underlying function
   * Higher order function contracts
      * Can define a function that defines constraints on the function that it takes as an argument

## The Cool Thing ##
   * Using a single command it all goes away
      * `(set! *assert* false)`

## Programs Writing Programs Writing Programs ##
   * Minderbinder
   * Inspired by Frink [http://futureboy.us](http://futureboy.us)
      * deals with units and unit conversions in a precise way
   * Unit conversions
      * just write a bunch of functions
      * keep typing
      * never stop typing
      * because there are so many different conversions!
      * "Ever feel like you're being boilerplated alive?"
   * Boilerplate
      * The number of tasks against unicorns
         * first time you do a task it takes a lot of unicorns
         * second time it takes less unicorns
         * third time, look at automating, might cost more unicorns but it's worth it in the long run
   * e.g., length specification
      * first time just write all the functions
      * then wrap it in parenthesis and make it look like Clojure, end up with abstractions that mean you don't need to write so many functions!
   * Primacy of syntax
   * Primacy of data
   * Mindbender
      * lets you just define the data and the conversions are implicit thanks to the macro
      * the macro does the calculation at compile time, the result of the macro is the result of the conversion

## Learn More ##
   * Books
      * ...
   * Links
      * ...
