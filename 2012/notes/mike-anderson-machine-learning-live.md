# "Machine Learning Live", Mike Anderson #

## Definition ##
* "Field of study that gives computers the ability to learn without
being explicitly programmed." - Arthur Samuel, 1959
* Learning: building functions from experience
* Examples:
  * Simple mathematical function: x -> y = sin(x)
  * Spam filtering: text of an email messgae -> probability of email
  being spam (%)
  * ...
* The state of machine learning: similar to the early days of flight.
  * It works...sort of...sometimes...on a good day...

## What do I do? ##
* nuroko.com
  * Building a toolkit for machine learning that is:
    * General purpose - ...
    * ...
## Why Clojure? ##
* Productivity and fun!
* Good parts of the JVM
* Interactive experiments via the REPL
* Functional programming
* DSLs with composable abstractions

## Key Abstractions ##
* Vector - efficiently represents information as a vector of double values
* Coder - converts arbitrary data into vectors (and back again!)
* Task - represents a problem to solve - typically ...
* Module
* Algorithm

## Neural Networks
* Node + weighted connections between those nodes
* Layers
  * Input layer
  * Output layer
  * Hidden layers
* Calculation goes from input to output layer

## How to Train a Neural Network ##
* Initialise network with some random weights
* Choose a random training example as input
* Compute the output
* Determine error (difference vs expected output)
* Adjust the weights very slightly to reduce the error
* Repeat from second step

## Demo: Teaching Scrabble Letter Scores ##

## Demo: OCR of characters ##
* Trick: Compress data
* Effectively the identity function for a neural network
* Compress to fewer nodes then decompress

## Questions ##
* How do you learn general solutions rather than just being able to
work with training data?
  * One of the best ways is to get more training data
  * Training data can be generated from existing training data by
    slightly modifying it
* Performance?
  * Options: use Clojure data structures, use Java data structures,
    use optimised libraries, use GPUs.
  * Desired benefits of the JVM mean sticking with optimised libraries
* How do you choose the neural network structure?
  * It's a bit of an art  
  * You can do it scientifically, randomly generate networks and test
    them out.



