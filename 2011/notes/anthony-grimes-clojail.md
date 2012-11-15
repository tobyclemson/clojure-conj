# "Clojail", Anthony Grimes #
[Slides](../slides/anthony-grimes-clojail.pdf)

## Background ##
   * Code is dangerous!
      * read and write to file system etc.
   * We need it to be, couldn't do stuff otherwise
   * Don't normally care about sandboxing
      * we are our own sandbox
      * don't let anyone else execute code on your system
   * Clojure allows code to be eval'ed from wherever you want

## The JVM Sandbox ##
   * Thorough
   * Prevents I/O
   * Denies access to certain methods and classes
   * Not enough for every single use case

## Sandboxing Clojure ##
   * Sandboxing state of Clojure is the hard part
   * Redeffing, infinite looping etc.
   * TryClojure, 4Clojure, LazyBot - allow user entered clojure

## How? ##
   * Look at namespaces symbols, classes vars etc.
   * Def - can abuse memory
   * Loops - timeouts!
   * Threads - can be used to avoid timeouts, must die
   * The dot `(.)` special form
      * Can abuse Clojure's Java
      * Cannot be got rid of
      * Cannot be rebound as it is a special form
      * Must be replaced entirely

## Why stop there? ##
   * Extensibility
      * Safety not the only concern
      * Customised evaluation contexts
         * Allow users to block whatever they want

## Clojail ##
   * Takes advantage of JVM sandbox
   * Sandboxes the Clojure side of things
   * Does very selective blacklisting
   * ...
   * Provides configurable sandboxes
      * Anything evaluated in the sandbox is subject to the sandboxing rules
   * `(sandbox ...)`
      * takes a set of things like Java classes, packages, symbols, sets, namespaces -> testers
   * `clojail.testers`
      * a selection of testers e.g., `secure-tester`
   * `(sandbox*)` - dynamic sandboxes, choose the testers on each evaluation
   * Sandbox automatically destroys long running executions
      * timeout can be specified
   * Defs
      * max-defs determines how many things can be deffed
      * anything over max-defs is undefined
   * Each sandbox is its own namespace
      * namespace can be set when sandboxes are created
   * Secure dispensations
      * clojail.jvm
      * can define a security context and associate it with a particular namespace
      * can independently sandbox the jvm using (jvm-sandbox ...)
   * Can evaluate things in the sandbox at creation time - available thereafter on the sandbox
   * Can bind to anything in the sandbox from outside thus hooking in
   to activity in the sandbox

## Implementation ##
   * Steps:
      * 1. Separate and Check

         * macroexpand most things
         * convert resulting structure to a collection
         * flatten the collection
         * process each element and check against testers...?
      * 2. Modify to sandbox anything missed before evaluation
         * e.g., replace `(.)` special form
         * use tester, check against object, fail if tester not satisfied
   * Timeouts:
      * execute inside a future with a timeout
      * stop thread group if timeout exceeded
   * Threads:
      * timeout handles basic threads `(Thread. ...)`
      * doesn't solve the threadpool problem...secure tester tries to
   * Evaluator:
      * in the context of the sandbox namespace
      * evaluate the code
      * use context of bindings
      * use jvm sandbox rules as well.
   * `(sandbox* ...)` ties it all together
      * rebind `*ns*` to the sandbox namespace
      * refer clojure (if true) inside the namespace
      * evaluate an init function which sets up the namespace however you want
      * store init-defs and custom dot macro
      * return function wrapping code, tester and bindings
         * initialise with jvm tester and clojure tester
         * execute above steps over code being added to the sandbox
         * wipe the namespace of any defs that shouldn't be there

## Summary ##
   * Not always enough
   * Take every precaution available
   * JVM sandbox is good but not infallible
   * Run code in its own user account
   * Goal is to safely evaluate code in the same namespace

## Usage Guidelines ##
   * Always use JVM sandbox
   * Update clojail regularly
   * Always report any issues
   * Avoid sharing the same namespace with everybody
   * ...
