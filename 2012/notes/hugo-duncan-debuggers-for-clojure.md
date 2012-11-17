# "Debuggers for Clojure", Hugo Duncan #

## History ##
* ...

## nREPL ##
* https://github.com/clojure/tools.nrepl
* REPL Client <-> Clojure process
* transport (socket & bencode)
* middleware stack
* Driven by Chas Emerick

## Middleware ##
* Client sends `{:op "load-file" ...}`
* Clojure nREPL server uses load-file middleware and sends back `{:status "done"}`
* Client can display notification
* Support for Clojure and ClojureScript

## Leiningen Profiles ##
* Configure your favourite middleware in `~/.lein/profiles.clj`
* `{:user {:repl-options {:nrepl-middleware [ritz.nrepl.middleware.doc/wrap-doc]}}}`
* Or add project specific middleware in project.clj
* `:dev {:repl-options {:nrepl-middleware [ritz.nrepl.middleware.doc/wrap-doc]}}`

## Clients ##
* Reply: Colin Jones, [on GitHub](https://github.com/trptcolin/reply)
* Counterclokcwise: Laurent Petit
* VimClojure: ...
* nREPL.el 
  * An Emacs client for the nREPL protocol, unfettered by other lisp implementations...

## Ritz ##
* [Ritz](https://github.com/pallet/ritz)
* Started life as a form of swank-clojure, but is now a very different codebase
* Initially just nREPL support but now supports SLIME too

## Ritz Components ##
* ritz-swank
* ritz-nrepl
* ritz-debugger
* nrepl-middleware
* repl-utils

## Ritz Debugger ##
* Refactored after reading "Out of the Tar Pit", Ben Moseley, Peter Marks 2006.
  * Isolate mutable state
  * Provide simple data query and update ops
  * No preferred access path
* Map for each connection, with assoc and update-in functions for different areas within the connection

## Ritz Debugger Middleware ##
* nREPL client <-TCP/IP-> Debugger Middleware (nREPL Server) <-JDI-> User Middleware (nREPL Server)
* Could be used by other (non-Emacs) clients
* Emacs package for nrepl.el extensions

## Using Ritz nREPL Debugger ##
* Install `nrepl-ritz.el` Emacs package
* Add `lein-ritz` to your `:plugins` in leiningen profile
* Run `lein-nrepl` and connect using host and port from Emacs

## Demo ##

## What's Caught and What's Not ##
* Any `(try ... (finally ..))` block means that JPDA considers and exception within that block as caught.

## Jump to Source ##
* Linking source code to stack frames requires that the source is on the classpath
* The Ritz servers arrange this if the source is in your local repository
  * `lein pom`
  * `mvn dependency:sources`

## Compile Without Locals Clearing ##
* Lazy seqs get nilled out when a function invocation goes out of scope
* Can compile without locals clearing to avoid this

## Miscellaneous ##
* Can run lein commands from inside the user process in Emacs using `nrepl-ritz-lein ...`
* `nrepl-ritz-threads`
* Project support
* debug-repl for nrepl coming soon

## Future Direction ##
* Parity with ritz-swank
  * Breakpoints
  * Inspector
* Scriptable debugging

## Conclusion ##
* nREPL middlware provides flexibility
* Make Ritz the goto place for middleware and debugger.
