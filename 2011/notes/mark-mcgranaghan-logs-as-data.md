# "Logs as Data", Mark McGranaghan #
[Slides](../slides/mark-mcgranaghan-logs-as-data.pdf)

## Background ##
   * Everything is data!
      * Code as data
      * HTTP requests as data
      * Html markup as data
      * Exceptions as data
      * SQL queries as data
      * CLI options as data
      * Decision trees as data
      * Build spec as data
      * Cloud deploys as data

## Logs as data? ##
   * Possible power vs. current power -> big gap
   * Data via simple abstractions with a general library

## Data as the fundamental unit ##
   * Maps!
   * Avoid hiding data in micro interfaces which prevent easy manipulation
   * Use simple abstractions instead which are implemented by data dtypes
      * map, seq, fn
   * General library
      * `(->> foods (filter :hot?) (sort-by :cost) (...))`
      * `(useful.find-first tasty? foods) ;; third party functions easily usable`

## Logs ##
   * Simple abstractions?
      * XML log4j configuration? No!
      * Data selection
      * Formatting
      * Interfaces
   * General library?
      * No, primitives are wrong
   * Get very complete libraries that miss the point of generality
      * `org.apache.log4j.LogRecordFilter`
   * Unix
      * `grep` / `awk` / `sort` / `head`
      * Useful stuff!
   * Logging almost synonymous with strings and usually physical files on disks
   * Logging is a record of what's going on in your application
   * Better model -> events
      * stream of everything that is happening
      * record of everything that ever happened
      * extremely general!
   * API: (emit <event>)
      * e.g., 
         * `(emit (:level "info" :viewing true :user_id 24 :path "/home"))`
   * Library: `map` / `fn` / `seq*`
      * e.g., 
         * `(->> events (filter :viewing) (count-by some-fn) (timechart))`
   * Log lines -> events
   * Strings -> maps
   * Files -> streams
   * Log crunching -> event processing
   * Flow:
      * Emitters -> IA (Interfaces / Aggregators) -> Consumers
      * `(f event-stream)` -> This is just a function over the event stream generated

## Consequences ##
   * For:
      * debugging
      * auditing
      * metrics
      * analytics
      * alerting

## In Use ##
   * This has been implemented at Heroku
   * Makes it easy to generate dashboards that aggregate across multiple services
   * These update in real time based on the event data
   * Implementation - `heroku/pulse` - [https://github.com/heroku/pulse](https://github.com/heroku/pulse):
      * Hosts emit events
      * Event stream split and distributed to many receivers which execute statistical fragments
      * Resultant data sent to a merger
      * Merger emits statistics snapshots to the web clients

## Going Forward ##
   * maps + seqs : Clojure
   * events : ?
   * Events span process boundaries
   * What is the killer app for events?
      * pervasive unified event collection
      * event processing service -> place for Clojure to shine?
         * esper 
         * hadoop 
         * cascading 
         * cascalog 
         * storm 
         * conduit

## Questions ##
   * How do you handle errors within the event processing system itself?
      * Since these are mission critical logs it is ok to discard some if there are errors
   * This has focussed on events in the abstract sense, what about loading logs out of text files?
      * For the legacy systems inside Heroku, we load a log line and immediately transform it into an event to continue down the event stream pipeline
   * Do you distribute using TCP or UDP? How do you handle zero consumers
      * TCP, the aggregator is able to handle he case of zero consumers
   * The aggregator seems a lot like a generic message queue - have you considered using one?
      * Logbus and Pulse are both open sourced. We've not considered a message queue thus far.
   * How do you distribute code to the various nodes in the logging network?
   * Do you wish you could send dates as something other than string? (Rich Hickey)
      * Not sure of an implementation but yes it is a problem.
