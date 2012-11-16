# "Production ClojureScript", Paul deGrandis #

## Motivation ##
* What makes Clojure great?
* Clojure manages risk better than any other technology
* Do the advantages we gain through Clojure translate to the problems
faced in the places where ClojureScript would be used?
* Overview:
  * Risks and metrics
  * Thought process for adopting clojurescript
  * Options and strategies
  * Practitioner's overview
* JavaScript has reach
* Why ClojureScript?
  * Clojure as a data format
  * The reader

## A Tale of Two Systems ##
* Stack 1
  * Python + JavaScript
  * NGINX as reverse proxy
  * 17 classes, 56 functions
  * One month prototype, three months productionised
* Stack 2
  * Clojure + CLJS
  * Jetty
  * 4 namespaces (8), 9 functions (21)
  * One week prototype, one month productionised

## Defects - Complexity ##
* "Software needs seat belts and airbags", Berger 07/2012 [ACM]
* Defect removal efficiency before delivery: 85%
* Total cost of repairs: 1/3/ (budget + schedule)
* Root cause incidental complexities

## Getting Stung: General ClojureScript Risks ##
* ClojureScript is young
  * CLJS development cycle is short/fast
  * Missing protocols/libraries
* Exceptions and debugging
* Interactive development
  * Can use Clojure environment for CLJS development
  * Beware differences between Clojure and ClojureScript

## Validation ##
* Simple questions
  * What are the quality attributes?
  * What are the system constraints?
  * What's your biggest problem?
  * Where do you waste the most time/money?
  * Where/what are the risks?
* The whys:
  * Why ClojureScript?
  * Why not X?
  * Why, why, why?
  * Swap!

## New Horizons ##
* Hammock driven development in action
  * Can't handle read load
    * Unnecessary dynamism
  * Design-to-template dance
  * Constant SEO updates
  * Mobile growing fast
* Solution
  * Cache?
    * Still have design to template dance
    * Still have constant SEO updates and mobile is growing fase
    * Unnecessary dynamism
    * Cognitive load
  * Alternative?
    * Make the site static
    * Load templates from CDN
    * Load CLJS from the CDN for dynamism

## Protocols ##
* ClojureScript, shoreleave (pub/sub, browser)
* Adaptability, modifiability
* Loosely coupled code, inverted control
  * Bug in CLJS? Just fix it in line
  * Use exiting protocols to extend browser concepts, for example,
    local storage

## When In Doubt...Server ##
* There's nothing wrong with pushing stuff back into the server
* Use Clojure data between the client and server and then moving stuff becomes easier

## It's Not JavaScript ##
* Treat it like Clojure
* Use this to get around some of the JavaScript difficulties
