# Lightening Talks #

## "An Idea That Had Me", lovemachine ##
   * Cyclic time
      * cron 
      * tried writing something better
      * failed
   * Time
      * single dimension
      * uncountably infintely many instants
      * we tend to break it into ranges of well known size
   * Wrapped java.util.calendar
      * `(periods :month)`
      * `(bounded-cycles-in nov :day)`
   * Other fun
      * retrieve our concepts of "natural" boundaries
      * Predicates for testing human names, e.g., "is this month july?"
      * Conume either java.util.Dates or Longs
   * Parting thoughts:
      * Please play with monotony, [http://github.com/aredington/monotony](http://github.com/aredington/monotony) or add `[monotony "0.0.1"]` to your project.clj
      * Forks and issue reports welcome on github!
      * Dig through your old ideas and play with them in Clojure

## "Immutant - An application server for Clojure", Jim Crossley ##
   * Who are we?
      * Jim Crossley and Toby Crawley
      * TorqueBox
      * ...
   * JBoss AS7
      * App Server = "middleware"
      * Includes web, like Jetty or Tomcat
      * But also: messaging, caching, clustering, scheduling, transactions and more
      * Traditionally requires a large, bloated bag of annotated Java and XML
   * TorqueBox
      * Encapsulates JBoss with JRuby
      * Fastest Ruby deployment platform
      * Tuby + YAML instead of Java + XML
      * Version 2.0 due soon
   * Immutant
      * Only two months old
      * Web and core messaging implemented
      * Isolated deployments
      * Controlled via Leiningen plugin
   * immutant.clj
      * `(ns yourapp.init)`
      * `(:require [yourapp.core :as your] [immutant.messaging :as msg] [immutant.web :as web]))`
      * `(msg/start "queue/work")`
      * ...
   * Integrated polyglot
      * Ruby in the front, Clojure in the rear
      * Inter-language messaging
      * Uniform deployment
      * Simple horizontal scaling
   * Resources
      * [http://immutant.org](http://immutant.org)
      * #immutant
      * @immutants

## "Lispsters", ... ##
   * Who's familiar with the Arduino?
      * [most people in the room]
      * it's a microcontroller like the pic or ARM
      * great platform for prototyping devices
   * Can't use Lisp for Arduino programming currently
   * So we implemented a Lisp for the Arduino
      * from the ground up
      * not that easy but a good learning tool
   * Tech specs
      * 2K ram - enough for 15 tweets!
      * lexical scope
      * first class functions
   * Uberlisp!

## "Korma: Tasty SQL for Clojure", Chris Granger ##
   * Started out with ORM but found it was limiting in its abstractions
   * Instead wanted to use Clojure
   * Korma
      * Allows you to define databases and entities and perform queries in Clojure
         * `(defdb prod (postgres {:db "korma" :username "db" :password "dbpass"}`
         * `(defentity ... (hasone ...))`
         * `(select ...)`
      * Composable
      * Basically a SQL generation engine
      * Aim was to be flexible but not get in the way too much (as something like Hibernate does)
      * Built for real world stuff
         * Don't make assumptions
         * When I do they are overridable
      * Very small at its core
      * Can be used just to generate queries, don't necessarily have to execute
      * [https://github.com/ibdknox/Korma](https://github.com/ibdknox/Korma)

