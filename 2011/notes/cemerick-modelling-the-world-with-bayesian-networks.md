# "Modelling the World Probabilistically Using Bayesian Networks in Clojure", Chas Emerick #
[Slides](../2011-slides/cemerick-modeling-the-world-with-bayesian-networks.pdf)

## Me ##
   * @cemerick
   * Clojure full time since 2008
   * ...

## Why Bayesian networks? ##
   * Lots of modelling options
      * Hand curated, developed via Monte Carlo methods, or both (or other)
   * No black boxes
      * In contrast with neural networks where the weights mean nothing
      * Can determine the root causes for individual inferences (why do you think X?)
      * Can integrate with other systems at any level
   * Optimisable

## Books: ##
   * "Modelling and Reasoning with Bayesian Networks", ...
   * "Causality", Judea Pearl
   * "Probability Reasoning in Intelligent Systems", Judea Pearl

## Domains and Applications ##
   * Building incomplete representations of the world and making inferences based on incomplete, erroneous and noisy data
      * Process control
      * Decision systems
      * Prediction
      * Classification
   * Document analysis
      * e.g., SEC filings
      * variety of ad-hoc formats, systematically extract data from them

## How ##
   * Select features (random variables)
      * e.g., wet, rain, season, sprinkler
   * Appeal to logic
      * Truth tables
      * ...
   * Sometimes logic isn't enough
   * Joint probability distribution
      * For each combination of values (in the truth table), determine the probability
      * This can be used to determine `P(A|B)`

## (Bayesian) Probability in 1 Minute ##
   * `P(wet|spring) = (P(spring|wet) * P(wet)) / P(spring)`

## JPDs don't scale ##
   * 4 random variables -> 16 worlds
   * m^n worlds (m number of states, n random variables)
   * {spring, wet, sprinkler, rain} -> 2^4 = 16 worlds
   * 20 vars x 3 states -> 3.487e9 worlds
   * Need a better representations

## Bayesian Network ##
   * Directed acyclic graph of random variables showing a model of dependencies, network build by hand?
      * i.e., you know that rain is likely to make the lawn wet not that a wet lawn is likely to make it rain
   * Each node has its own probability table constructed with knowledge of what its parent is
   * `O(n log_m(p))`! That's good.

## Where's the f#&@£! Clojure? ##

## Raposo ##
   * Clojure library for Bayesian inference and modelling
   * Reimplementation / extraction from existing application
   * Clojure-idiomatic treatment of data
   * Learning vehicle
   * Data:
      * `[#{:rain :wet} #{:rain} #{:sprinkler :wet} #{:rain :wet} #{:sprinkler} ...]`
      * `(defprotocol Observed (features [this]) (value [this feature-name]))`
      * `(extend-protocol Observed clojure.lang.IPersistentSet ...)`

   * Modelling the world:
      * Basically:
         * `(def model (create-model {:rain #{:wet} :spring #{:rain :sprinkler} :sprinkler #{:wet} :wet}`
         * ...
      * Monte Carlo methods aswell:
         * `(def model (create-model [... probabilities ...] ...))`
         * ...
   * Query
      * `=> (probability-of :wet model [{:rain 0.9 :sprinkler 0.6}])` -> 0.84...
      * `=> (probability-of :wet model [{:sprinkler false}])` -> 0.48...
      * `=> (probability-of :rain model [{:wet true :sprinkler true}])`

...

## Raposo TODO ##
   * Release
   * Expose network learning / generation
   * Optimisation
      * Elision of independent random variables
      * Compilation
         * Bayesian network => Clojure
   * Integrate with core.logic

## Questions ##
   * Were Bayesian networks an area of general interest or was it specific to this problem?
      * No mostly just for this problem
