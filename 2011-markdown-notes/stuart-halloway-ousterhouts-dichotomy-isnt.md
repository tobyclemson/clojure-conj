# "Ousterhout's Dichotomy Isn't (Part 2 of the Simplicity/Power/Focus Series)", Stuart Halloway #

## Simplicity, Power, Focus ##
   * Last year, Simplicity
   * This year, Power
   * Next year?

## Power ##
   * Definition: to be able
   * Would be nice to give context to that
   * What about physics?
      * `P = IV`
      * `P = dW/dt`
         * the amount of work you can get done over the amount of time you spend
         * work per unit time
         * work has a direction, towards something thus not towards everything else
         * work smarter not harder
   * What about computer scientists?
      * expressive power
         1. automata power
            * finite automata
            * pushdown automata
            * linear bounded automata
            * Turing machine
            * Turing oracle
         2. moving down this list you become more powerful in terms of things you can express
         3. functional power
            * pure untyped lambda calculus
            * lambda calculus with constraints
            * ...
         4. logic power
            * zeroth order logic
            * first order logic
            * higher order logic
            * datalog
               * with negation
            * prolog
         5. model power
            * declarative languagues
            * + dataflow variables
            * + laziness
            * + cells
         6. poetry power
            * sonnet
            * haiku
            * rhymed couplets
            * blank verse
            * free verse
         7. music power
            * the trombone is strictly more powerful than the piano
               * free to play between tones
            * guitar more powerful than trombone
            * piano more powerful than guitar
            * huh?
      * rock/paper/scissors/lizard/spock!?
   * Expressiveness vs. work done per unit time

## How do we categorise power? ##
  1. Whose time?
      * Powerful means different things to different people
      * A machine manages power to accomplish a task
  2. ...
      * Things my stakeholders never ask for:
         * Turing completeness
         * Decidable type system
         * Laziness
         * Negation
         * ...
      * "Writing free verse is like playing tennis with the net down"
      * "When publishing on the Web, you should usually choose the least powerful or most easily analysed language variant that's ..."
  3. Composition
      * x considered harmful
         * goto
         * global variables
         * mutability
         * dynamic scope
         * explicit memory management
      * feeling of power comes from combining and constraining expressive powers

## Osterhout's Dichotomy ##
   * Overloaded distinction
      * static vs. dynamic
      * complex data structures vs. limited data structures
      * compiled vs. interpreted
      * independent programs vs. glue code
      * C, C++, Java vs. Tcl, Ruby, Python

## Revenge of the Nerds ##
   * Most languages:
      * Have: 
         * conditionals
         * function type
         * recursion
         * dynamic typing
         * garbage collection
         * expressions
         * symbol type
      * Don't have:
         * homoiconicity
         * whole language all the time
         * values
         * identity
         * polymorphism
         * etc.
   * Lisp / Clojure does have those things.

## Measuring Abstraction Powers ##
   * Concision
   * Locality
   * Simplicity
   * "It's not clear that Paul Graham's list of power concepts works for anything other than selling one startup to Yahoo Stores"

## Revenge of the Glue ##
   * static vs. dynamic
   * complex data structures vs. complex data structures
   * compiled vs. interpreted
   * independent programs vs. glue or independent
   * C, C++, Java vs. Tcl, Ruby, Python, Lisp?

## Foreign Function Interface ##
   * ...

## What's not glue? ##
   * static vs. dynamic
   * complex data structures vs. complex data structures
   * compiled vs. interpreted
   * independent programs vs. glue or independent
   * C, C++, Java vs. Tcl, Ruby, Python, Lisp?

## Platform Power ##
   * Need:
      * classes
      * interfaces
      * primitives
      * byte codes
      * core types
      * library types ...
   * Don't need:
      * static typing
      * compilation model
   * Clojure aims to provide full platform power
   * "I Didn't right clojure to replace Ruby in my day job, I wrote it to replace Java in my day job" - Rich

## Platform Power Explains ##
   * `reify/proxy`, et al
   * 1.2 -> `protocols`, `deftype`
   * 1.3 -> numeric changes
   * absence of wrappers
   * Clojure / ClojureScript differences
   * compromises with simplicity

## Numeric Options ##

<table>
        <tr>
                <td></td>
                <td>safety</td>
                <td>speed</td>
                <td>type</td>
                <td>precision</td>
        </tr>
        <tr>
                <td>checked</td>
                <td style="color: green">safe</td>
                <td style="color: green">fast</td>
                <td style="color: green">any</td>
                <td style="color: red">limited</td>
        </tr>
        <tr>
                <td>promoting</td>
                <td style="color: green">safe</td>
                <td style="color: red">slow</td>
                <td style="color: red">boxed</td>
                <td style="color: green">arbitrary</td>
        </tr>
        <tr>
                <td>unchecked</td>
                <td style="color: red">unsafe</td>
                <td style="color: green">fastest</td>
                <td style="color: green">any</td>
                <td style="color: red">limited</td>
        </tr>
</table>

## Instructive Exceptions ##

   * integer byte code operations
   * creating interfaces
   * implementation inheritance

## Library Power ##
   * does library exist?
   * can I find the library?
   * ...

## Can we have a small shot of easy? ##
   * Error messages Rich? :)
   * Life would be easy if:
      * ...
   * Feeling powerful
      * expressive power
         * core (red)
         * library (green)
      * platform power (red)
      * library power (green)
      * ease (green)
   * Changes to all things in red have to go through Rich
   * Changes to all things in green are community driven
   * Adding comforts should be paralleliseable
      * shouldn't have to go through Rich
      * modular contrib now community owned
   * Comfortable needs to be there in development, slim and speedy for production

