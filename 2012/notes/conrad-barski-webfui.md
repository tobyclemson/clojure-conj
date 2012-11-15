## "Webfui: A functional, client-side UI framework for ClojureScript", Conrad Barski ##

## Definitions ##
* What is the DOM?
  * Mutable object representation of the document in the browser
* What is EDN?
  * Syntax expression
  * JSON
* What is AJAX?
  * Client server communication after the page has loaded

## Goals ##
* Do things the "Clojure way"
* Functional programming
* The DOM should be EDN stored in an atom
  * Want it to look like hiccup

## Main Parts of Webfui ##

### webfui.dom ###
* Takes Clojure atoms and syncs them with the browser DOM
* Capturing user interactions:
  * Watches vs. events
    * Just want before and after rather than complex event object
    * Familiar in the Clojure world as you can attach watches to atoms
    * "Show me, don't tell me"
* Automatically updates DOM based on watches
* Diffs old vs. new DOM and only updates based on delta    
* Making webfui.dom pleasant to use
  * Browser DOM -> DOM Atom -watchers-> World State -render-all-> DOM
    Atom -> Browser DOM

### webfui.state-patches ###
* Allows you to write a description/diff of how you want the state to
  change and it will apply it for you.
* State changes are usually *highly localised*
* DOM changes are usually *global*  
* 3 parts to a diff:
  * Things that have been added
  * Things that have been edited
  * Things that have been deleted
* `(patch state diff)`: effectively a recursive map merging function

### webfui.plugins ###
* Dealing with user actions that don't change the DOM
  * Make "hidden" DOM changes more visible
    * The DOM is more rich than what you can express in HTML
    * You have to use JavaScript to access those parts of the DOM
  * Add additional types of watches (i.e., event handlers)

## AJAX With Webfui ##
* Approach 1: Maintain a request queue in the state atom
  * No. You really only want to deal with things that have an
    instantaeous lifetime
* Approach 2:
* World state vs. other state
* Treat server communication as a virus
  * System things its state is the whole world
  * Something external tells the system it is corrupt
* How to handle a virus:
  * Get lucky!
  * Contain it
  * Cure it
