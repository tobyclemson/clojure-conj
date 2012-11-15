# "Introduction to Logic Programming", Ambrose Bonnaire-Sergeant #
[Slides](../2011-slides/ambrose-bonnaire-sergeant-introduction-to-logic-programming.pdf)

## Introduction ##
   * Outline
      * Fundamental logic programming concepts
         * Related to FP
      * General implementation characteristics of LP languages
      * Gain an understanding of the execution model of `core.logic`

## Pure Functions ##
   * Pure functions (in FP)
      * Functions always have one value -> deterministic
      * Works for only one pattern of input and output arguments
   * Sometimes functions are inappropriate
      * e.g., 4 has two square roots, +2 and -2
         * 2 results
      * e.g., dividing a number by zero yields no result
         * 0 results

## Relations ##
   * Generalise functions to get relations
      * Any number of results -> non-deterministic
      * Pattern of input and output arguments can be different for each call
   * Mathematically, an expression '`X r Y`' is true if `X` and `Y` satisfy relation '`r`'
      * e.g., '`X < Y`', 4 ways the '`<`' relation can be considered:
         * A generator of the (infinite) set of all `(X, Y)` pairs for which `X < Y`
         * A predicate that can be applied to `(X, Y)` pairs
         * A generator that, given `X`, will yield all `Y` values greater than `X`
         * A generator that, given `Y`, will yield all `X` values less than `Y`
   * Converting function to relation
      * Relations return true if the relations is true and false if the relations is false
      * To convert a function to a relation
         * convert the return value to an argument:
            * `(cons 1 [2]) ;=> [1 2]`    goes to    `(cons 1 [2] [1 2]) 1 2]) ;=> true`
