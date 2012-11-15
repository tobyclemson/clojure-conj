# "LightTable", Chris Granger #
[Slides](../slides/...)}

## Background ##
* Recently entered Node.JS Knockout
* JavaScript competition, want to write a game in ClojureScript
* Traditionally games written in an object oriented way with huge
  object trees.
* Component Entity System
  * Component = State
  * Entity = ID
  * System = Logic
* Example:
  * `(component position [x y a]
      :x x
      :y y
      :a (or a 0))`
  * ...
  * Need to map Entity => Component ID
  * `(component renderable [func]
      :fn func)`
  * `(defn renderer [renderables]
      (doseq [e renderables]
      (let [rend (as e :renderable)]
      ((rend :fn) e))))`
  * ...
* Data all the things
  * Data structure represeting state of game at a given time
  * Functions
* Get composition as a result
* See slides for example
* What about being fast?
  * Why is this difficult in ClojureScript
    * Things change a lot
    * Need to iterate over entities a lot
    * Seqs can't go that fast in ClojureScript
    * Persistent collections not slow to write to but they are a GC nightmare
  * We have access to JS arrays and objects
    * These are very fast
  * We have macros, we can make JS arrays and objects look more "Clojurey"
* Data + composition
* End result
  * About 2300 lines of code
  * 500 - 1000 lines of game definition
  * All in all about 700 lines of game code
  * Not bad...painful to get there
    * Exceptions very difficult to understand and debug

## So what about LightTable ##
* Written in ClojureScript almost completely
* Using node-webkit [on GitHub](github link)
  * Embeds node.js inside Chromium
* LightTable uses Component Entity System under the covers
* ...
* Behaviour Object
  * Behaviour = event handler
  * Object = `{:state}`
* Everything in LightTable is an object
* `(object/object* ::console
    :triggers []
    :behavious []
    :init (fn [this]
        (console-ui this)))`
* Behaviour
  * `(object/behavior* ::on-click-rem!
        :triggers #{:click} ...)`
* Data
  * ... notification example
* Composition
* All of LightTable is just one big data structure
  * Introspection for free
  * Runtime configurability

## Conclusions ##
* LightTable is probably the biggest ClojureScript codebase in the
  world right now
* What needs to improve in ClojureScript?
* 5 wishes:
  1. Better errors
  2. Compiler on node
  3. CLJS analyzing CLJ
  4. Screencasts
  5. Better tools

## Questions ##
* There was a big shift in the design of LightTable early on in the
  project. Why was that?
  * We wanted to get to everything as data and functions to get back
    to total editability of the IDE
* Have you thought much about plugins and user configurability
  * Yes, everything we can do you can do
  * We are looking to build something akin to emacs but fully graphical
* If the state data structure is the interface for plugin writers
  aren't you at risk of backwards incompatibility?
  * Changes should be relatively infrequent
  * We could always shim if keys change
* Does that state data structure include anything non-serialisable?
  Would it be useful to have it serialisable?
  * Serialisation is important since it would be nice to sync the
    state between running LightTable instances
  * The whole data structure doesn't need to be serialisable, a view
    would be sufficient.

## Random thought ##
* Nice idea to have a service that you talk to in code.
