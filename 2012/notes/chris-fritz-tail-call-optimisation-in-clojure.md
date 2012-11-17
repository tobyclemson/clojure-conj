# "Tail Call Optimisation in Clojure", Chris Fritz #

## Outline ##
* A little history
* Built-in TCO support in Clojure
* Enter CTCO
  * Coninuation Passing Style (CPS)
  * Thunkification
  * Trampolining
* Some fun optimisations
* ...

## Goals ##
* High-level understanding of CTCO transformations
* New outlook on continuations
* An idea of costs and benefits of CTCO

## Un-Goals ##
* Not showing CTCO internals
* Not creating CPS experts

## Current Year: 1977 ##
* Imperitive languages rule the land
  * Fortran, PL/1 etc.
  * Lisp exists for academics

## A Sinister Debate ##
* Structured programming vs. GOTO

## Setting the Record Straight ##
* Guy Steele: "Lambda: the Ultimate GOTO"
* Dear compiler writers: don't be dumb about procedure calls

## Tail Calls Are Special ##
* List example: 
  * `(define (bar x y) 
      (f (g x) (h y)))`
* Stack:
  * 1st frame: `(bar x y)`
  * `(g x)` -> r1 in a frame
  * `(h y)` -> r2 in a frame
  * `(f r1 r2)` ?
  * Reuse 1st frame as nothing in there is needed
* Last function call deosn't need a new stack frame
* Tail calls are like a GOTO with arguments

## Tail Calls Are Awesome ##
* Efficient and natural way to iterate
* Steele & Sussman included constant space tail calls in Scheme standard
* Later adopted by Standard ML
* Seem like a great idea for every language ever

## Not So Fast ##
* Not every language ever includes constant space tail calls
* Java security model requires stack frame for every call

## Built-In TCO ##
* For self-recursion: `recur`
* For arbitrary tail recursive chains: `trampoline`
  * Requires manual transformation
  * Get to that later

## Build It Better ##
* CTCO does all the work
* Takes the burden off of programmers
* Result is as good as (or better than) manual transformation

## Part 1: CPS ##
* What a continuation does:
  1. Takes a value
  2. Does computations waiting to happen
  3. Returns a value
* Think of it as a function
* Empty continuation `(fn [v] v)`

## Big Claim ##
* Continuations === Stacks

## Factorial Example ##
* CPS version
  * `(defn fact [n k]
      (if (zero? n)
       (k 1)
       (fact (dec n) (fn [v] (k (* n v))))))`

## Part 2: Thunkification ##
* Wrap every function call in a `fn` of no orguments, or "thunk"
* Breaks a computation into steps
* Prevents runaway stack growth

## Factorial Example ##
* Thunkified version
  * `(defn fact 
      ([n a] (fact n a (fn [v] v)))
      ([n a k]
       (if (zero? n)
        (k a)
        #(fact (dec n) (* n a) k)))))`

## Part 3: Trampolining ##
* Runs a computation step-by-step
* Implemented within a looping construct
* Figure out when to dismount

## Factorial Example ##
* Trampolined version
  * `(defn fact 
      ([n a] (tramp (fact n a (fn [v] v))))
      ([n a k]
       (if (zero? n)
        (k a)
        (with-meta #(fact (dec n) (* n a) k) {:thunk true}))))`

## CTCO In Summary ##
* CPS makes the stack explicit
* Thunkification prevents runaway stack growth
* Trampolining runs the computation to completion

## Costs of CTCO ##
* Creating and passing functions for continuations
* Creating and invoking thunks
* Stack vs. heap memory

## Optimisations ##
* Auto-recurify
* Arity collision problem

## Future Work ##
* Plug remaining holes in accepted language
* Port to ClojureScript
* Write `tools.cps`
* Abstract interpretation for minimal thunkification

## References ##
* "A First-Order One-Pass CPS Algorithm" by Olivier Danvy
* "Using ParentheC to Transform Scheme Programs to C or How to Write Interesting Recursive Programs in a Stack-Based, Imperative, Inhospitable Host" by Ron Garcia, Jeremy G. Siek, Heather Roinestad, and Daniel P. Friedman
