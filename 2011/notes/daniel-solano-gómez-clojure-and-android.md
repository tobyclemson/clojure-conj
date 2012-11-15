# "Clojure and Android", Daniel Solano Gómez #
[Slides](../2011-slides/daniel-solano-gómez-clojure-and-android.pdf)

## Overview ##
   * Android and the Dalvik VM
   * Dynamic Compilation
   * ...

# What is Android?2 #
   * Software stack for mobile systems that provides an operating system, middleware and ...
   * Android architecture
      * Linux kernel
      * Android runtime
      * Libraries
      * ...
   * The good news
      * Lots of reuse
   * The bad news
      * JavaVM != Dalvik VM

## Java VM vs. Dalvik VM ##
   * Differences
      * JVM: 
      * Dalvik:
         * Not much cpu power
         * Not quite Java SE 2
         * .class files
         * ... see diagram
   * .class file:
      * Header
      * Constant Pool
      * Other data structures / ...
   * Createing a DEX
      * Multiple classes
      * Same header
      * Same constant pool
      * Independent data structures
   * Installing the application
      * .dex file optimised to .odex
   * Consequences
      * Loading bytecode in android is a heavy-weight process
      * Dynamically loading bytecode is not currently supported
   * Android Programming languages
      * Dynamic
         * ...
      * Compiled
         * ...

## Dynamic Compilation on Android ##
   * Why?
      * Makes a Clojure REPL possible
   * Review
      * `(defn hello [name] (str name ...)`
   * A new class Loader: `DynamicClassLoader`
   * Split into
      * `JVMDynamicClassLoader`
      * `DalvikDynamicClassLoade`r -> does extra work
         * class -> ...
   * Choosing the right `DynamicClassLoader`
      * New var: `clojure.core/*vm-type*`
      * New dependency
   * Android compatibility
      * Doesn't work on versions prior to 2.1
   * Clojure compatibility
      * All Dalvik-related code is loaded reflectively
      * Some complex macros may not compile due to size limitations
      * `clojure.core/bean` not available due to lack of `java.beans` API
   * Performance
      * Compared Clojure, Java, Scala, Ruby
      * Package size
         * Preferably keep it low due to data network limitations and device storage
      * Startup time
         * How long do I have to wait for something to appear on the screen
      * Heap size
         * The more it takes up, the less you have for you application
   * Where did all the time and space go?
      * `clojure.core`
      * top space hogs
         * `__init` : due to meta data
         * namespaces
         * input and output streams
      * what about time?
         * the first time something is run, there is a 7.8s overhead
         * most of this comes from loading the runtime
            * load clojure core namespace
            * create user namespace
         * lots of garbage collection going on
         * 300% object churn
         * comes from metadata
   * How do we improve performance?
      * Remove user namespace
      * Remove metadata
      * Transients during initialisation
      * Serialisable `clojure.core`
      * Source-level tree shaker

## What would help Clojure Android development? ##
   * Neko: The Clojure/Android toolkit
      * easy object-oriented/function impedance mismatch
      * reduce boilerplate
      * ...
   * Development tools
      * ...
   * Android development version of Clojure
      * needs to be upgraded to 1.3
      * merge into upstream Clojure?
   * Build tools
      * Neko provides helper for Ant / Android SDK
      * Would be nice to see more mainstream build tools
   * REPL / dynamic development tools
      * Would be good to see tools like nrepl, Emacs etc. integrated

## What about ClojureScript? ##
   * Should work for web apps
   * Might work with mobile development frameworks
   * For native development, constrained by availability of JavaScript engines
   * Should work with scriptiing layer for android but doesn't provide ideal "native experience"

## Android and Clojure ##
   * Clojure has the potential to be a first-class language for Android development
   * Dynamic development on Android is a killer feature
   * It needs better tool and community support
   * Book pending: "Decaffeinated Android", building Android apps
   without using Java

## Questions` ##
   * Even without load time, GCs seem to be very frequent, kills UX,
      * Early Androids weren't very good
      * The introduction of concurrent GC has helped a lot
   * Have you tried running regular Clojure with your changes to see if it improves performance?
      * Not really, however I don't think the things I've done would impact non Android development
   * Startup time is a real problem on Google App Engine, any performance improvements in startup time would be very useful in that space...
      * Probably true.
   * Right now on Android, when it builds an app, a lot of work goes on besides generating the DEX file, there's also resource generation etc. What's your build environment and how do you handle this extra stuff?
      * Modify compile target to do Clojure compilation as well as Java compilation

