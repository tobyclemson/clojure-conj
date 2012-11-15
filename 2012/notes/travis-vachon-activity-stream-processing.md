## "Monsters, Daemons and Storms: Adventures in Activity Stream Processing", Travis Vachon ##

## Act 1: Web Scale ##
* Copious.com
* Building a social marketplace
* Lots going on: like things, unlike things, share things, buy things
etc.
* The feed is the core of copious, similar to the news feed in face
book
* Users:
  * Associated to other users
  * Associated to other people's things
* Actions -> stories -> aggregated into peoples feeds
* Initially used mongoDB in the background
  * `{actor: 'rob', listing: 'guy-with-bear', action: 'loved',
    interested: [travis bear]}`
* Eventually fell over
  * Growing "interested" embedded docs can lock the database
  * Queries required scannign embedded doc
  * Query optimiser made some bad decisions
  * ...

## Act 2: Set Theory ##
* Reasoning:
  * Sets of stories about people and listings
  * Feeds are unions of those sets
  * Choose sets to union based on interests
* Ended up going with redis
* Interests
  * Stored in a set
  * Entries are types and ids of interests
  * Entries mapped to stories
  * Stories aggregate into feeds by user
  * Feeds generated dynamically at runtime
* Hoped it was going to be scalable enough to get through the next six
  months...it wasn't.
  * Too many interests -> Too many story sets
  * Too many story sets -> Slow union ops
  * Unions (almost) always slow ...
  * ...

## Act 3: The Many Armed Daemon ##
* The problem:
  * Feeds can't be built fast enough at runtime
  * So, maintain all feeds in redis
  * Use Ruby? Needs to be fast...
  * Clojure daemon reads from Resque
  * Updates interests, stories, feeds
* New requirement: digesting
  * Roll stories up
* Difficult to solve:
  * Can't read 70k+ feeds from redis for each story, so we maintain head
    of feed in memory
* Solution:
  * Take head of each feed, put into atom, store in memory
  * Write out to redis later
  * Allowed parallelism to be increased
* Problems:
  * Slightly dangerous to process multiple actions at once so tons of
    bottlenecks
  * Initial feed builds, sotry add, interest adds all in same process
  * Need to make it as fast as possible
* Threads:
  * Thread to stick stuff into new feeds
  * Thread to time stuff out
  * Thread to edit stuff
* Optimised by breaking the atom up into smaller more focussed atoms
  to avoid collisions
* Conclusions:
  * Clojure was awesome for this
  * Fast
* Still problems:
  * Storing all feeds in redis memory: expensive
  * Feed builds are only mostly fast, so can't rely on them for onboarding
  * Not at all robust, if daemon breaks or needs GC nap there is
    nothing you can do.
    * ...
* Storm:
  * Spout, stream tuple, bolt, serialisation, deserialisation
  * Tuples: just bags of data
  * Spouts:
    * Poll external sources and emit tuples
    * Acknowlede successful processing
    * Handle failure
    * Enable reliability
  * Bolts:
    * Raw processing power
    * Receive tuples from streams
    * Arbitrary logic - query dbs, download internet, whatever. Can carry
      state
    * Emit tuples back to streams
    * Lots of parallelism
  * Serialisation
    * Arbitrary serialisations
    * Falls back to Java serialisation
    * Just Works out of the box
    * Lots of power under the covers
  * Allows you to define stream groupings
* Success!
  * But wait...how do we do feed rebuilds?
  * Storm has a DRPC server that can trigger topologies
  * DRPC is just story primitives
  * Plays nicely with normal storm topology
  * No longer need to store all feeds in redis, cut down storage by
    95%
      * Shut down massive redii
      * ...
* Conclusions:
  * Clojure rocks!
    * Easy parallelism
    * Clean code
    * Libraries available
    * Fast and capable
    * People build stuff like storm
  * Mostly...
    * Mature, idiomatic library support
    * JVM is the worst (except for all others)
    * Laziness will bite you at some point, especially when working
      with stateful DBs
    * ...
      
