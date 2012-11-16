# "Further Adventures of Leiningen", Phil Hagelberg #

## Introduction ##
* Leiningen was born in 2009
* Written after using Maven for a Clojure project and experiencing
  lots of frustration.
* Version 2 has been a chance to revisit the decisions made in version 1.
* Rectification of names - first mistake was calling Leiningen a build
  tool, in fact it is a project automation tool.
* Problems with being just a build tool:
  * No launcher for Clojure, leiningen now serves that role, not
    really a build responsibility
  * Trouble with a build tool as a launcher is that it has ideas about
    tests etc.
  * Profiles helps to alleviate this
* Other problems with version 1:
  * REPL was sucky, now using nrepl as a unified interface to the REPL
  * Dependency management had issues

## Project Description ##
* `(defproject ...)` -> `{...}`: it's a macro but the output is just a
  map
* lein-keyprint plugin will produce the map if you need to see what it
  looks like
* Benefit of being just a map is you can use plain old map
  manipulation on your project definition

## Tasks ##
* Think about them in terms of functions
* `lein hello x y z`
* `(apply (fn hello [project & args] ...)
    {:name "marabunta", :group "marabunta" ...}
    [x, y, z])`

## Dependencies ##
* Referential transparency
* Notion of snapshots
  * Project having a snapshot is like having dynamic bindings
  * Version ranges (testing against clj 1.3 to 1.4)
    * If you specify 1.4 and a dependency specifies 1.3-1.4 then your
      version will be ignored
    * Avoid version ranges
  * lein-pedantic plugin: refuses to resolve dependencies if there is
  any ambiguity.
* Standalone JARs
  * Can use .m2 repository or S3 bucket
  * lein-local-repo plugin: allows you to install a standalone jar to
    a local repository
  * However these are only addressing the real issue of a JAR not
    being available in a public repository.
  
## Repository/Dependency Security ##
* Practically non existent.
* Easy to perform a man in the middle attack for dependencies
* JARs can be signed and maven central requires it however this is
  rarely checked.
* `lein deps :verify` will tell you the signature state of your dependencies
* Signantures are a start but since the keys for signing are not
  centralised this isn't enough
* Need to build a web of trust in the community to manage distributed signing
* Work is being done on a new Clojars repository to act as a releases repository

## GPG ##
### GPG Basics ###
* `gpg --gen-key # expire in 2 years`
* `gpg --send-keys $KEY_ID`
* Sign artifacts upon deploy
* Encrypt stored credentials

### GPG Key Signing ###
* Write down thier name and key fingerprint
* Check their identification
* `gpg --recv-keys $KEY_ID`
* `gpg --fingerprint $KEY_ID #confirm match`
* `gpg --sign-key $KEY_ID`
* `gpg --send-key $KEY_ID`

## Questions ##
* What were some of the problems you found with using Clojure with
  Maven? Were they deep seeded problems with Maven itself or was it
  just the Clojure Maven plugin?
  * The usual compile, test, package aspect of Maven doesn't make
    sense for an interactive language
* Currently leingingen 2 is separated into leiningen core and a
  separate shell. Is there a plan to merge them in future?
  * The reasoning for this is that the core can be pulled in by IDEs
    whilst the task definition remain in a separate project.
  * Plumbing in one place, task definitions in another.
