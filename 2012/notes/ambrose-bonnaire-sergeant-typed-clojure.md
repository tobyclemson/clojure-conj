## "Typed Clojure"

## Verifying Clojure code ##
* Popular program verification techniques in Clojure:
* Unit testing (clojure.test)
* Design by contract (pre- and post-conditions)
...

## Why static typing? ##
* Static typing can check certain invariants more effectively than
other techniques
* Code written in abstract programming styles (e.g., Monads, Arrows,
Conduits) are well suited.
...

## Goals ##
* Should understand most Clojure idioms
  * Porting should not require extensive restructuring of code
* Should allow mixing of typed and un-typed code
* Type checking should be optional
  * Can still run code even if type checking fails
* Should not require custom compiler
  * "Typed code" ...

## Existing Work: Typed Racket ##
* Typed sister language of Racket
* Supports many Racket idioms
* Provides safe interoperability between typed and un-typed code
* ...

## Typed Clojure ##
* An optional static type checker for Clojure
* Based on Typed Racket
  * With Clojure-specific extensions
* Developed for:
  * ...

## Overview ##
* - Code > Analyser Compiler - AST (Java Objects) -> Analyze - AST
(Maps) -> Typed Clojure - AST (Typed) -> ?

## Getting started ##
* [on GitHub](frenchy64)
* ...

## Running the checker ##
* `(check-ns)` or `(check-ns nsym)` checks a namespace
* ...

## What to annotate ##
* The usual rules with local type inference
  * All global vars that are referenced or are defined in typed
    namespaces need annotated types
  * ...

## Annotating vars ##
* `(ann var type)` ...

## Annotating functions ##
* `(ann-form form type)` ...
* `(fn> ...)`

## Union and Intersection types ##
* Untagged union `(U ...)`
* Intersection `(I ...)`

## Type aliases ##
* AKA abbreviations
* ...

## Universal Quantification ##
* ...

## Instantiating Type Parameters ##
* ...

## Function types ##
* ...

## Occurence typing ##
* Conditional
* ...

## Variable-arity ##
* Uniform variable-arity
  * e.g., +,-
* Non-uniform variable-arity
  * e.g., map, mapcat, swap!
* Keyword parameters
  * Not yet supported

## Maps ##
* Maps with known keyword keys can be expressed as a heterogeneous map
  type that record the presence of keyword keys
* Potential extensions: See O'Caml record types, row polymorphism,
  record concatenation

## Heterogenous maps ##
* ...

## Datatypes & Protocols ##
* `(ann-datatype ...)` gives a type to a datatype
* `(ann-protocol ...)` ...
* ...

## Java Interoperability ##
* Typed Clojure utilises Java static type for interactions with Java
* `nil` is separated as a static type, therefore so is `null`
* ...
