# "Challenges from Logic Programming", Steve Miner #

## Prologue: Last Year at the Conj ##
* Dan Friedman and William Byrd - miniKanren
* Ambrose Bonnaire-Sergeant - core.logic (ported by David Nolen)
* Jim Duey - recent fork/join work

## Outline ##
* Personal experience
* Historical narrative
* Boring filler
* Dramatic conflict
* Unsatisfying ending

## Challenge ##
* An objection or query as to the truth of something often with an implicit demand for proof
* Why learn logic programming?

## 25 years ago ##
* A lisp programmer
* Expert systems and planning
* Discovered prolog

## AALPS ##
* Automated air load planning system
* Loadmaster: logistics, restraints, weight, balance
* Army-wide standard for cargo-aircraft load planning and analysis
* Small team of Prolog programmers at SRI

## Cultural Challenge ##
* Common Lisp
  * S-exprs, macros, CLOS
  * Full control
* Prolog
  * Strange syntax
  * Unification and backtracking

## Logic Programming ##
* Inspired by logic
* Facts, rules, queries
* Defining relationships between objects
* Computation is deduction

## The Art of Prolog ##
* Leon Sterling and Ehud Shapiro, 1986
* "In Prolog programming (in contrast, perhaps, to life in general) our goal is to fail as quickly as possible"
* Shapiro: Concurrent Prolog
* Consulted on Fifth Generation Project

## Benefits ##
* Precise problem statement
* Elegance
* Declarative semantics
* Procedural execution
* Flexible and transformable
* Verification by proof (maybe)

## The Fifth Generation ##
* Artificial intelligence and Japan's computer challenge to the world
* Edward A. Feigenbaum and Pamela McCorduck
* Edward Feigenbaum:
  * Knowledge systems lab at stanford
  * 1994 ACM Turing Award for AI work
  * IntelliCorp and TekKnowledge

## The Fifth Generation ##
* Japanese governemnt sponsored
* Parallel hardware
* Prolog based software
* Natural language interface
* Knowledge information processing system (KIPS)

## Mixed Reactions ##
* Feigenbaum saw US falling behind
* IBM didn't care
* Lisp hackers were skeptical
* Prolog proponents anticipated success
* Europe had cut back on funding CS
* DARPA - AI Winter is coming

## Development of Logic Programming ##
* Paper by Carl Hewitt, 2008 (many versions)
* What went wrong
* what was done about it
* what it might mean for the future
* Carl Hewitt
  * Planner language (1969)
  * Procedural embedding of knowledge
  * Actor model of computation
  * Direct Logic (TM)
  * ...

## The Birth of Prolog
* Alain Colmerauer on Planner
* "The lack of formalization of this language, our ignorance of list and, above all, the fact that we were absolutely devoted to logic meant that ...""

## What Went Wrong ##
* Clausal form hides the underlying structure of the information
* Practical domains of knowledge are inconsistent
* Proof by contradiction is not a sound rule of inference for inconsistent systems

## Unifying role of Logic Programming ##
* Kowalski "Computation could be subsumed by deduction"
* Pat Hayes: "Computation = controlled deduction"
* ...

## Failure of Fifth Generation Project ##
* High risk approach
* Consortium wasn't totally committed
* Hardware was late
* Natural language interaction wasn't ready
* Parallelization and committed choice
* Prolog took the blame

## Logic Inspired ##
* Languages: Concurrent Prolog, Mercury, Oz, Prolog, Shen, miniKanren, core.logic
* Constraint logic programming
* SAT solvers
* Rule-base systems (OPS5, CLIPS, Drools)
* Datalog

## Clojure Can Help ##
* Community
* Functional programming is a good host
* Dacts, rules, even models can be values
* Run everywhere + the browser
* Concurrency

## Meeting Challenges ##
* Awareness
* Prove usefulness to engineers
* Beyond toy problems
* Clojure adoption
