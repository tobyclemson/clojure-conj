# "Computable Stories", Kovas Boguta #

## Introduction ##
* "Most of our systems live outside of the bounds of any single
  process we write", Rich Hickey
* The complexity from the broader system can reach into our system and
  make this more difficult.
* For example the complexity inherent in databases
* Humans are part of our systems
* But:
  * No information model
  * No process model
  * No notion of update
  * No conveyance
* Blowing our foots off
* Forgetting what we did
* Can't share knowledge
* Disaster of unmanaged state
* What's the Clojure way for human computation?
* Narrative is where humans meet computation
* Basic observation:
  * Computation is a narrative
  * ...
* Why we care
  * Narrative is the most powerful form of communicating knowledge
  * Humans operate on narratives
* Session is a system for narrating computations

## Computational Stories as a Value ##
* Perceive
* Remember
* Fabricate
* Reproduce
* Convey
* Index

## What Stories Do For Us ##
* Stories explain
* Stories instruct
* Stories convey purpose

## What's the Biggest Problem in Clojure? ##
* Documentation
  * According to 30% of respondents to the 2012 State of Clojure
    survey by Chas Emerick

## Instructional Session ##
* Examples, without the incidental complexity
* Better for the author
* Better for the reader/user
* Much easier to share, index

## Explanatory Session ##
* Reproducible
* Advantages over an application

## Session Architecture ##
* User
* UI
* Datomic
  * Action -> result
* Services
  * Consume and produce facts  

## Components ##
* Process model
* Services
* Location independence for data
* Lean on values

## Services ##
* Not just Clojure evaluation! APIs, etc.
* Interact with services via transactions
* Tell them to make stuff and report back
* Tell them to coordinate with each other
* Services as a value?

## Location Independence ##
* Critical for sound information model
* Critical for conveyance
* Implementation detail, managed by datoms
* `[[result :session.result/location loc]
    [loc :result.location/host host]
    [loc :result.location/protocol p]
    ...]`

## Lean on Values ##
* Benefits are enormous
* Things like graphics, UI
  * Perception independent of state
* Abstracting away location, services
* ...

## Comparison With Other Systems ##
* REPL
  * DIY conveyance
    * PLOP
  * Transcription erros
  * No versioning
  * No context
  * No extension of environment
* Smalltalk
  * Not smalltalk images
* Mathematica
  * Not documents/notebooks

##  Paradigm Whose Time Has Come? ##

