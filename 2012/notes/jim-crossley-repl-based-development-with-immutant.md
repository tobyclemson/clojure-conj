# "REPL-Based Development with Immutant", Jim Crossley #

## Immutant Runtime ##
* Application server for Clojure
* Built on top of JBoss
* Why would you want a Clojure application server
  * Exposes commodity services such as caching, messages, clustering
    etc. to your Clojure application
  * Other libraries exposed on top
  * Supports Leiningen

## The Challenge ##
* Having a REPL in the deployed environment to gain access to
  everything the production app would have access to

## Demo: Poorsmatic ##
* For a given set of search terms, find matching Tweets that contain a
link.
* Identify the links with the highest frequency of the same search
terms.

## Data Flow ##
* Web UI
* Database
* Terms (topic)
* URLs (topic)
* Twitter daemon
* URL scraper

## Cluster View ##
* Twitter daemon, URL scraper etc. will be clustered.

## Live Coding Demo ##
* Emacs + Slime + Immutant
