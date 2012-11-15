# "(Neal's) Master Plan for Clojure Enterprise Mindshare Domination", Neal Ford #
[Slides](../2011-slides/neal-ford-clojure-masterplan.pdf)

## Background ##
 * Get to talk to lots of CTOs and might be able to bring some perspective and context
 * Going to focus on mu rather than lambda, the coefficient of friction!

## How do... ##
 * things become popular?
 * you make things popular?
 * ...

## How do things become popular? ##

### Rain down from the top ###
 * Build Your Own Technology Radar
    * The ThoughtWorks radar covers the technologies TW thinks are hot explaining some of the more controversial members
    * Technologies are organised in a ring with the outside being don't use (hold) and the center being should use (adopt)
    * Build 2 radars? One for developers, one for CTOs
 * Litmus Test for Choosing A Technology
    * How do you determine the next big thing?
    * Developer radars and litmus tests are all over tha map
 * CTO Litmus Tests
    * Must be able to hire tons of inexpensive developers
    * The flaw here is that often you can achieve the same or more with a small team of high skill developers as with dozens or hundreds of lower skill developers
    * This statement really means "I'm afraid"
    * Often choose the less effective but more industry standard approach
    * Need to mollify CTOs and make them less afraid of the idea
    * Get them to risk success instead of avoid failure
 * How do we '#mollify'?
    * Create new Clojure-ists everywhere
    * Sponsor SICP user groups
    * Create a poignant guide
    * Lurk around schools!
    * Koan contests
    * Make Clojure commonplace - make it a building block people use without even knowing.
 * CTOs don't fear lisp
    * They don't even know what lisp is!
    * They fear "different"

### Sprout up organically from the bottom ###
 * Productivity Pirates
    * Don't care about cool tech, they care about getting stuff done as quickly as possible
    * Build tools that support productivity pirates, raise the productivity flag
 * How do we '#hoist'?
    * Web framework (boring)
    * RESTful integration?
    * O/R mapping?
    * Rules engines?!?
 * 2 Ways:
    * Breaking and entering
       * e.g.,
          * Linux
          * Rails
       * Forced their way into the enterprise
       * Very difficult to do, has to be incredibly compelling
       * Need to give the impression it's not too risky
    * Cat burglary
       * Piggy back your techology in on the back of another technology
       * e.g.,
          * Ruby on the back of Cucumber
          * Groovy on the back of Gradle
          * XML on the back of [pretty much everything!]
 * How do we '#camouflage'?
    * Make Clojure commonplace
    * Get the clojure.jar everywhere

## How do you make something popular? ##
 * Be like Fox news! 
 * Propaganda: a form of communication that is aimed at influencing the attitude of a community towards some cause of position so as to benefit oneself or one's group
 * How do we '#propagandise'?
    * Stay on message!
       * High performance
       * Simple, not easy
       * Clojure as a vision for software, not a language
       * [Pimp the knitted castle vs. lego castle!]
    * Stay relatively positive
       * e.g., Charles Nutter with JRuby convinced the Ruby community

## How do you build a bridge to popularity? ##
 * Bringing a gun to a knife fight!
 * We have Lisp!
 * '#packheat'
    * If you believe you have an advantage...
    * ...prove it!
 * How do we '#packheat'?
    * Know you enemies
       * Not agile
       * Not scala
       * It's the status quo
 * '#befriend'
    * Scala will be the Next Big Thing on the JVM because it fetishizes complexity exactly the way that Java developers are used to.
 * How do we '#befriend'?
    * Sell
       * alternate language to Java
       * functional
       * dynamic
    * Now we can talk Clojure
    * Celebrate Scala's success - "A rise in tide raises all ships"
 * '#encapsulate'
    * Encapsulate the entire world, they're not going to build a bridge to you, you need to build a bridge to them
 * How do we '#encapsulate'?
    * Wrapper everything?
       * Add a nicer API around, for instance, the Actor library in Scala
       * Similarly, wrap all the Java APIs in an idiomatic Clojure way

## Neal's Master Plan ##
 * #packheat
 * #mollify
 * #propagandise
 * #encapsulate
 * #camouflage
 * #hoist
 * #befriend

## Success Stories ##
 * Spring
    * started small
    * strategised - SpringSource
    * brought in people to solve the difficult problems
    * infiltrated!

## Questions ##
 * Why should we engage the enterprise? Is it a lost cause? Should we just focus on the small startups that are more likely to adopt?
    * The trouble is you don't get the same kind of penetration if you take that approach
    * As a community you need to decide whether you even want to penetrate the enterprise
 * But if businesses are built using Clojure that might make it easier for enterprise to adopt...
    * Exactly, mollify.
 * Is it really a social problem? Why not just build a tool that translates between Java and Clojure?
    * Please build one, I'll take it into all the enterprises I work in
 * Ruby went in without any baggage in the 90s, how do we shed out Lisp baggage?
    * The people you need to sell to don't know about Lisp's baggage
    * The baggage isn't necessarily a bad thing
    * Separately, having all the infrastructure, tools and libraries available makes the baggage unimportant
 * One of your first premises is that organisations want low cost people, Clojure doesn't align with that, how do we handle the inexpensive people problem?
    * We need to push the "get more done with smaller teams" argument
    * Ruby is helping in this respect since Ruby teams are usually smaller
 * I think you're missing the point, organisations aren't going to fire all their existing people, they need to upskill them
    * Yes that's a good point, that's why you need to make Clojure-ists everywhere
 * It's all nice and good wanting to be in the enterprise but we shouldn't forget that there's also tonnes of money there!
    * Exactly right, that's precisely what the Spring guys saw, make money, build more stuff
