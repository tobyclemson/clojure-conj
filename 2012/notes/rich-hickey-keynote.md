# "The Language of the System", Rich Hickey #

## The Language Bubble ##
* Programming language defines world (with Runtime)
* I/O as if someone else's problem vs. the point of your program

## Language + Runtime ##
* Memory model
* Calling conventions
* Resource management
* Coordination
* Abstraction
* Types
* ...

## System ##
* Stand together
* Ensemble of programs (services)
* No global managers as with runtimes/OS
* Connected how?

## Language ##
* 'Tongue' - communication, programmer -> programmer
* Programming language - programmer -> computer
* System language - program -> program

## The Stacks ##
* Program
  * Application libraries
  * Runtime and core libraries
  * Language primitives
* System
  * Application as services
  * ? 
  * Protocols and formats

## Say What? ##
* XML, JSON, Protocol buffers, Avro, edn, Hessian, BERT
* All data, but:
  * Extensible? to new types, new versions
  * Self describing?
  * Schemas? explicit? in/out of band?
  * Generic processors and intermediaries?

## Values ##
* Most often ephemeral, on wire
* Need names when not:
  * passing large values
  * memory
* How to distinguish value from reference?
  * Permalinks etc.

## Names ##
* Global scope
* Namespaces critical
* Very few used for 'code' or verbs
* Services, machines, storage locations etc.

## Read Between the Lines ##
* Where do the semantics of a system live?

## The Revenge of Objects ##
* DANGER!
* 'Service' is an arbitrary notion
* Triggering effects across a graph of stateful services (== objects)

## Welcome to the Machine ##
* Machines apply force to accomplish work
* That's what systems do

## Avoiding Objects ##
* Transform (values)
* Move (values)
* Route (values)
* Record/remember (values)
* Keep separate
* Flow vs. places

## Transform ##
* Values on I/O straightforward
* But sometimes work from/to storage

## I'm a Mover ##
* Queues rule
  * Decouple producer and consumer
  * Identity and availability
* Move/route values
  * Pub/sub etc.

## Memory ##
* Epochal time model still works
* References (identities) to values
* Coordination a la carte

## Epochal Time Model ##
* Identity (succession of states)
* Observers/perception/memory
* ...

## Datomic on Riak ##
* + Zookeeper

## Failure ##
* Partial
* Independent
* Timeouts
* Retries, idempotency
* [Read this paper, multiple times](http://www.erland.org/download/armstrong_thesis_2003.pdf)

## Systems are Dynamic ##
* Membership
* Capacity
* Capability
* Discovery, scalability, elasticity etc.

## Holistic Approach ##
* e.g., Erlang
* Fundamental language units are services
* Bespoke communication
* Specified model (actors)

## Heterogeneous Approach ##
* Cross-language/runtime/platform
* ...

## The Stacks ##
* Program
  * Application libraries
  * Runtime and core libraries
  * Language primitives
* System
  * Application as services
  * *Simple services*
  * Protocols and formats

## Simple System Services ##
* Communication (message queues)
* Coordination (ZooKeeper)
* Control flow (AWS Simple Workflow, Storm)
* Memory (memcache, redis etc)
* Storage (S3, K/V stores et al)
* More, and smaller - the best do the least

## Whither the Interface? ##
* What abstracts away service details?
  * Not much (IDL, WSDL etc not common)
* De facto standards get copied
  * S3, memcache
* Can do this in programming-language libraries
  e.g., jclouds, abstraction over storage and machines aspect of AWS
* System equivalent of this abstraction is a proxy but that adds a hop
  so you don't see it often.

## Programs -> Systems ##
* Need more values if we want FP benefits
* Flow orientation and fine granularity encourage reuse and
composition
* Interfaces/abstraction
  * lives where?
  * without this, it is difficult to parameterise service with services

## Systems -> Programs ##
* Recognize machine-like portions of programs
* Build human interfaces atop programmatic
* System failure model is the failure model
* Systems are dynamic and data driven
  * Is your language?
  * Are your protocols?

## Call to Action ##
* Consider building simple services rather than language libraries
* Try to avoid bespoke protocols and formats
* Consider the abstraction of your service
* Design to be composed
