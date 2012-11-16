# "Clojure Data Science", Edmund Jackson #

## Part 1: Background ##

### Background ###
* Data science: statistical analysis of data using computation.
* Alan Turing was originally a data scientist

### Available Tools ###
* Excel
  * Most widely deployed analysis tool on the planet
  * Unfortunately possessed by a demon paperclip who will turn your
    floating point numbers into dates
* Matlab, Mathematica, R, Sas, Statter
* C++ and Fortran

### What do you need? ###
* Mathematical tools
  * Interactive environment
  * Visualisation
  * Linear algebra
  * Statistics
  * Machine learning
  * Optimisers
* Platform capabilities
  * Native language speed
  * Data structures
  * Language constructs
  * Data connectivity
  * End-to-end quality control
* Existing platforms and tools don't cover all bases
* Analytical power (depth)  vs. platform power (breadth)
* Python is the current state of the art
  * Good library support
  * Capable virtual machine

### More power? ###
* Functional programming
  * Immutability
  * Close to the maths
  * ...
* ...

### Why use Clojure? ###
* Clojure itself
  * Incanter
  * Storm
  * Cascalog
  * Datomic
* Interop
  * Rincanter
  * JNI
* The JVM
  * Mahout
  * jBLAS
  * Weka - machine learning package

## Part 2: Entropy Always Wins in the End ##
* British coin: heads (60%) vs. tails (40%)
  * The queen exerts a force on the coin so that her head is visible
  more often :)
* Generative distribution vs. measured distribution
* Unexpectedness
* Distribution over unexpectedness
* Gives entropy (unpredictability)
* Relative entropy (between 2 distributions)

### Demo ###

### What is Clojure lacking ###
* Native libraries
  * Linear algebra
  * Optimisation
  Statistics
* Numerics
  * No hope

### The Future ###
* Near
  * Libraries and ports
  * Session
  * Incanter 2.0
* Medium
  * Probabilistic programming 

## Questions ##
* What sort of things do you use for visualisation?
  * Mostly incanter even though it is a bit weak
* Why is relative entropy asymmetric?
  * Due to the p/q in the log.
