# "Extending JavaScript Libraries from ClojureScript", Kevin Lynagh #
[Slides](../2011-slides/kevin-lynagh-clojurescript-javascript-interop.pdf)
[Handout](../2011-slides/kevin-lynagh-clojurescript-javascript-interop-handout.pdf)

## Background ##
   * Found that:
      1. Clojure is simpler than JavaScript
      2. Using JS from ClojureScript is moar extendable than using JavaScript 
      3. .js -> .cljs is an adventure!
   * Consider Imperial :: Metric -> JavaScript :: Clojure

## Let's Talk About JS ##
   1. Clojure is Simpler Than JavaScript
      * "JS has a lot of stupid in it!", Brendan Eigh, creator of JavaScript, news at 11
      * What terrifies you about JavaScript?
         * The way the JavaScript defines variable scope etc.
            * Attack of the killer globals
               * `var x = 12;` vs. `x = 12`;
            * JavaScript programs tend to live in the browser alongside lots of other programs
            * Clojure solution: things don't change!
         * JavaScript Namespaces
            * `(function () { ... })();` 
               * module pattern is all we have! 
               * required to isolate your code from others
               * this is crazy!
            * Clojure solution: use Clojure namespaces
               * Never going to make it to the top of Hacker News because it is so boring
               * But that's a good thing, it should be boring
      * CoffeeScript will not save you!
      * So, Clojure is simpler than JavaScript
      * Myth: Only Geniuses use Functional Languages
   2. Using JS from ClojureScript is More Extendable
      * Interop review
         * `(. js/console log "hello")`
         * `(.log js/console log "hello")`
      * One difference
         * `(.aMethod js/anObject)`
         * `(. js/anObject (aMethod))`
      * Types:
         * Scalars are all native
            * CLJS string are JS string
            * CLJS numbers are JS numbers
         * Collections are foreign (lazy in CLJS)
      * JS objects
      * Reader literals
      * Compare
         * `jQuery.select("#main").append("<span>").text("hello);`
         * `(-> js/jQuery (. select "#main") (.append "<span>") (.text "hello"))`
      * The Clojure style is easy to extend as you can insert your own functions into the method call chain:
         * `(-> js/jQuery (. select "#main") (.append "<span>") (my-append "<blah>") (.text "hello"))`

      * The JS way:
         * Break the chain and call your own function
         * Or add a "plugin" -> `jQuery.fn.my_appender = function(x) {}`
         * End up building facades
      * e.g., 
         * `(defn append [sel node-type] (.append sel node-type))`
         * `(defn select [sel selector] (.select sel selector))`
         * `(-> js/jQuery (select ...) (append ...))`
      * So, using JS from ClojureScript is
         * more fun
         * more safe
         * more extendable
   3. What we thought we knew until ClojureScript showed us otherwise
      * Let's talk about this
         * `var f = function () { return this; }`
         * `f(); // -> DOMWindow`
         * `var dog = {};`
         * `dog.name = "Rex";`
         * `dog.bark = function() {return this.name;};`
         * `dog.bark // -> Rex`
      * Beware apply!
         * `(apply (. js/dog bark) 1 2 3)`
         * `cljs.core.apply.call(null, dog.bark, cljs.core.Vector.fromArray([1 2 3]));`
      * Referential transparency problems
      * Free unsolicited advice:
         * Tools don't make the artist

## Questions ##
   * Why D3? (visualisation library)
      * Most other visualisation libraries just give you a menu and you choose from it
      * D3 allows you to construct your visualisations however you want, rendering everything out in svg
