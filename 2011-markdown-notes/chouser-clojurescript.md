# "ClojureScript: Under the Hood", Chris Houser #
[Slides](../2011-slides/chouser-clojurescript.svg)

# Terminology #
   * Regular Clojure: plain old Clojure
   * CLJS: ClojureScript
   * GClosure: google closure (from closure compiler)

## ClojureScript Pyramid ##
```
   / data types \
  /   protocols  \
 /     macros     \
/     compiler     \
```

## Data Types ##
   * `[a b c]` - vector
      * `cljs.core.Vector`
         * `meta`: cljs Map
         * `array`: js Array
      * copy on write whole new vector on change
   * `{a 1, b 2}` - map
      * `cljs.core.ObjMap`
         * `meta`: cljs Map
         * `keys`: js Array
         * `strobj`: js Object of keys and vals
      * `cljs.core.HashMap`
         * `meta`: cljs Map
         * `count`: number
         * `hashobj`: js Object of buckets
      * difference is `ObjMap` is more sophisticated but less efficient
      * copy on write - whole new map on change
   * `#{a b c}` - set
      * `cljs.core.Set`
         * `meta`: cljs Map
         * `hash-map`: cljs Map
   * All implemented in cljs itself

## Protocols ##
   * cljs collections -> cljs protocols
   * No inheritance at all
   * In cljs, can take a type that we didn't write and extend it to adhere to cljs's own protocols
   * Not possible in regular Clojure without some sort of wrapper
   * What do you do if the type you didn't write already implements part of what you want to extend it with?
      * Overwrite and become authoritative
      * Leave existing implementation in place

## Macros ##
   * Steps:
      * analyse/macroexpand
         * gives a metadata decorated tree representing the input code
      * emit
      * load and run
      * loop
   * Macros are clojure code, all of this happens in the JVM

## Compiler ##
   * [Added a feature in 5 lines during the live demo]

## Miscellaneous ##
   * `(js ...)` - gives the JS equivalent of a Clojure form
   * `(js* "(~{}[~{}])" blah blah)` - string interpolation of args into format string
   * Unicode character used to separate keyword strings from symbol

## Questions ##
   * Are there any plans to make the core data types more like the regular Clojure data types?
      * Actually, regular Clojure data types are effectively copy on write for small collections
      * Probably no need at the moment for the same in CLJS
   * Are there any plans to improve the interop between CLJS and Javascript?
      * There has been some discussion on the google group


