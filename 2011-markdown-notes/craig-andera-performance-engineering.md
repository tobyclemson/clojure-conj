# "Faster, Baby: A Performance Engineering Experience Report", Craig Andera #

## Background ##
   * About me:
      * Work for http://thinkrelevance.com
      * Writes software
      * [github]
      * [twitter]
   * How do you approach performance engineering?
   * Model based optimisation
      * A way to look at your system
      * How to make improvements in performance the right way
   * Optimisation loop
   * How the Clojure system we worked on benefitted from this approach
   * Practitioner - this is just stuff that has worked for me

## Model Based Optimisation ##
   * What's wrong with this picture?
      * Near ship time, someone says, "Time to make it faster!"
      * You go to your users to get performance requirements
      * They make up a number
      * You make the system match that number
   * Here's what
      * Done late
      * Done haphazardly
      * Done in the absence of an adequate model
   * Performance is not a scalar quantity
      * "How fast is the system?" rarely has an answer
      * Your system probably doesn't do just one thing
      * The world is not deterministic!
      * Need a stochastic model of you systems's performance
         * involving randomness
   * Models!
      * Useful
         * What is the 99% case for response time when I have 10 users?
            * stochastic
            * average case
         * What will the system do if I get mentioned on HackerNews?
            * load testing
         * How many servers will I need a year from now?
            * capacity planning
      * Wrong!
         * Be aware of assumptions in the model
            * Testing versus production
            * Small versus large data
            * Load balances or not?
            * etc.
         * This is not an excuse for not doing this
         * How wrong do you have to be before it stops being useful?
         * "Remember that all models are wrong; the practical question is how wrong do they have to be to not be useful?" - George E. P. Box, Empirical Model-Building
   * One useful model
      * latency "distribution" versus throughput for a given transaction mix
         * don't focus on just one thing, mix up possible transactions to be representational
      * plus whatever other constraints you have
         * for instance cache expiry times
   * Use load testing
      * 1 users, then 2 users, then 3 users etc.
      * graph throughput, requests against time?
      * this doesn't give you the latency though...background time or wait time in each request
      * questions we can answer with this model:
         * Can we meet our customers expectations?
         * How much capacity do we need to handle spikes?
         * What is it going to cost us to run this system?

## The Optimisation Loop ##
   * Benchmark -> analyse -> recommend -> optimise -> loop -break-> done!
      * Benchmark
         * Do
            * measure the parameters of you model
            * remember that transaction mix is critical!
            * understand what you are measuring
         * Don't
            * mistake # of threads for load
            * forget to look for errors
            * keep going if you're done
            * wait to start
         * Tools
            * load generators: jmeter, ab, httperf
            * analysis: excel, Clojure!
      * Analyse
         * Identify the biggest factor in the perf of your system...empirically!
         * Generally this is done via profiling
         * And lots of hard thinking
         * Be aware of transaction mix
      * Recommend
         * You've found the one slowest thing
         * Often easy in the early rounds
         * This will get harder the longer you go
         * Now figure out what to do about it
         * Use the data!
         * The best recommendations is "We're done. Let's stop."
      * Optimise

         * Fix the one slowest thing
         * You may find redesign is necessary
         * This is why you want to start early
   * "Any problem in computer science can be solved with another layer of indirection", ...
   * "Except for the problem of too many layers of indirection", ...

## Real World Example ##
   * Where we started
      * About 75 req/s peak
      * About 25 ms avg latency
   * What we did
      * Prepped customer
      * Two-card iterative approach
         * One card is a combination of benchmarking and analysis
            * Output being enough data to come up with the recommendation card
         * Other card is a recommendation and optimisation
            * Output being the work involved in the optimisation and to come up with the next benchmarking card
      * Several rounds of optimisation
      * Over about a month
   * Where we got to
      * About 1700 req/s peak throughput
      * < 10 ms latency @ 1500 req/s @ 99% confidence
      * A very happy customer
   * Iterative approach helped them get to where they had wanted to be for 2 years in 1 month
   * Stuff that happened
      * Found out that logging was one of the bottlenecks
         * ~80% of time!

         * How?
            * Wrote a wrapper around the log library
            * This allowed the log library to be called from Java
            * This allowed the log library to be valled from Clojure
      * Found out a one-character change in a config file made a huge difference
      * Uncovered an issue with huge volume of log data
         * 2 Gbs an hour! 
         * Client wanted to keep all of that! Where!?
      * Later, had to redesign logging infrastructure again
      * Never tested load-balanced
      * Got stress test basically for free
      * Used automated load testing, tests ran overnight, emailed us in the morning

## Conclusion ##
   * Be deliberate
   * Think about your model and define it
   * Be stochastic
   * Recognise that the model is wrong
   * If performance optimisations are needed use the optimisation
   loop: measure : adjust : measure

## Questions ##
   * How do you verify that your benchmarks are testing what really matters?
      * What really matters is up to you
      * Rephrase: How do you tell whether your model is actually going to reflect what happens when you go live?
      * Build a model, work with the people who own the environments, ask if it's what they wanted
      * Use metrics, match up against model
   * Is there anything specific about Clojure that you learnt in this process?
      * Clojure wasn't a performance bottleneck!
      * Nothing about Clojure itself limited us
      * Mostly database caching and logging, syslog4j
      * Choose the right data structure for the job, linear access -> random access made a big difference in one case
   * Would you recommend building in iteration boundaries for optimisation or making it an organic part of the process?
      * The latter, make it a fundamental part of the development process
