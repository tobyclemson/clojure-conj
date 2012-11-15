# "Predicate Dispatch", David Nolen #
[Slides](../2011-slides/david-nolen-predicate-dispatch.pdf)

## Background ##
   * There was an email a couple of years ago saying it would be nice if multimethods worked in a slightly different way
   * Rich replied that what was being talked about was very similar to predicate dispatch
   * This sparked interest

## core.logic ##
   * Faithful miniKanren implementation based on William Byrd's dissertation
   * Performance oriented enhancements
   * Adds knowledge base facilities
   * cKanren enhancements coming up!

## Pattern Matching ##
   * "alphaKanren and nominal logic programming"
   * I didn't like the pattern matching macro in the dissertation
   * "Compiling Pattern Matching to Good Decision Trees"
   * Lazy Pattern Matching
   * Craig Chambers "Efficient Predicate Dispatch"

## Predicate Dispatch ##
   * Chambers (Self) & Chan
   * Some details are hardwired
   * How to remove the hardwired details?
   * Will it be dog slow?
   * Lots of other challenges
   * Rich Hickey doesn't like pattern matching!
   * ...
   * Then why bother?
      * This is not Java
      * If we're willing to do a bit of research, the language is
      malleable enough to add the feature yourself

## Why Predicate Dispatch? ##
   * What's wrong with multimethods?
      * They're really powerful :)
      * Don't use them often but they're nice to have when you do need them :)
      * The dispatch is hardwired :(
         * can't change that function in the future
   * Expressiveness, Simplicity and Power
      * Simple ideas are easy to adopt
         * Sophisticated ideas need a simple story to be impactful
         * "Deceptively simple"
      * Sophisticated ideas still need simple interfaces
      * Doing things dynamically instead of statically can be really
      liberating

## Is Predicate Dispatch Simple? ##
   * Is open dispatch simpler than closed dispatch?
   * `(defm ... [inner outer (form :when ...)] ...)`
   * Winding roads to predicate dispatch
   * Pattern matching
      * rich history of papers in the mid 80s
      * key enhancement predicate dispatch offers is open extension

## core.match ##
   * Matches arguments against predefined structures to determine result
   * Each pattern type is handed all rows that match
   * Maps give random access in matching that lists don't
   * Closed -> open simalar to static -> dynamic

## Open Extension ##
   * Pattern matching is top down
   * Open extension is not
   * `even?` implies 2
      * original paper hardwired numbers
      * can we avoid that?
   * Inserting some (core) logic
   * But we don't want to break other people's code (namespace local changes?)
   * e.g.,

      * `(defpred even? even?)`
      * `(defm foo [(x :when even?)] ...)`
      * `(defm foo [2] ...)`

## More Challenges ##
   * `core.match` being closed is simple - generate the correct static source
   * Supporting dynamism - performant implementation no longer simple 
   * If we change to a graph representation we lose the performance benefits of host branching primitives `(if ... else)`
   * Lazy compilation complicates targeting Clojurescript
   * We could emit the entire dispatch at each extension point - code size will suffer
   * Like `deftype` / protocols perhaps we could fully optimise all cases defined "together", future extension taking a reasonable performance hit
   * Grouped future extension receive shared performance benefits
   * What about redefinition? What about introspection?
   * Extension that require a reordeing - "game over", perhaps we emit the entire decision tree locally to the namespace?
   * Big idea: non-overlapping clauses
   * Other ideas / solutions / approaches
   * Wishful thinking is fun isn't it?! :)

## Questions ##
   * Checkout Charles Forgey with Ops 5
   * Is it production ready?
      * No not at all!
