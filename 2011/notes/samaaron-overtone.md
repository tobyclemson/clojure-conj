# "Notes on the Synthesis of Music", Samuel Aaron #
[Slides](../slides/samaaron-overtone.pdf)

## Background ##
   * Play on words from "Notes on the Synthesis of Form", Christopher Alexandra
   * "The Timeless Way of Building", Christopher Alexandrs influenced "Design Patterns" by the GoF
   * Also want to talk about Kasparov, being beaten by a machine, deep blue
   * What do you do when, as a chess grand master, you get beaten by a computer?
      * Started improving the computer
      * Focussed on psychology and tactics
   * "Weak human + machine + better process was superior to a strong computer alone and more remarkably, superior to a strong human + machine + inferior process", Gary Kasparov

## Music ##
   * First machine built to make music, sounded dreadful but was pretty amazing at the time.
   * Hasn't changed much since! :)
   * Came up with Improcess
   * Real goal is to be like Jimi Hendrix! Music as performance
   * Compare that the me and Jeff Rose playing on our laptops at the Ruby on Rails conference
   * What do we want to be able to do?
      * Improvise
      * Communicate
   * This can be bound together via an interface
      * Ableton Live

         * Existing software doesn't help to convey virtuousity
      * Notation
         * Easy to visualise what was intended
         * Easy to visualise lots of complex data
         * Sound waves don't really reveal much
   * Max Matthews
      * Recently died at 84
      * One of the fathers of computer music
      * Wrote: "The Digital Computer as a Musical Instrument"
         * Take a stream of numbers and turn them into sound
         * Discussed a notation for synthesis
   * Supercollider
      * Captures all of this in a box
      * Along with an API to send updates and events
      * Version 3 separated out the server from the language
      * "One goal of separating the synthesis engine and the language in SC Server is to make it possible to explore implementing in other languages ..."
   * Overtone
      * A frontend language to the SuperCollider Server
      * Focus
         * Live interaction and exploration
         * Abstraction building
         * Code generation
         * Toolkit implementation
         * Reald world connectivity
      * Concurrently and collaboratively manipulate patterns and beats
      * [https://github.com/overtone/overtone](https://github.com/overtone/overtone)
      * A bunch of other libraries have come out of it

## Interface ##
   * Code is one interface, we'll talk about that later
   * It's not always the best thing though
   * We need a physical device that allows us to interact in a more tactile way
   * e.g., 
      * TouchOsc - allows different interfaces for different use cases
      * Mono - square thing with a grid of light up buttons

## Demo ##
