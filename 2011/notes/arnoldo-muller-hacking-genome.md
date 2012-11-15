# "Hacking the Human Genome Using Clojure and Similarity Search", Arnoldo Jose Muller-Molina #
[Slides](../slides/arnoldo-muller-hacking-genome.tar.gzarnoldo-muller-hacking-genome.tar.gz)

## Background ##
   * Working in bio-medicine and stem cell research
   * Pioneering a process that can be applied to
      * Tissue reconstruction
      * Organ generation
      * Disease modelling

## Problem ##
   * Only know 10 or 20 % of transcription factors
   * What are transcription factors?
      * Proteins that attach to DNA
      1. Attach to the dna
      2. A lot of stuff happens
      3. A new transcription factor is "printed", other side effects are possible
      4. Attach again
   * TFs bind to specific DNA sequences
   * Gene:
      * Docking region: promoter
      * +
      * Blueprint region: coding region
   * What is a binding motif?
      * Representation of the set of DNA subsequences a TF can bind to.
   * Genes switch on and off with TFs
   * If you know a motif
      * You know where the TF binds
      * You know which genes will be switched on and off
   * Want to reverse engineer ...
      * ...
   * Objective
      * Find missing 2300 TF motifs

## Encrypted Message ##
   * Statistically analyse message and apply know facts to deduce message
      * e.g., the in English

## Motif finding problem ##
   * Difficult
      * 10% of dictionary available
      * No grammar
      * Only some of the message is useful
   * From ~2 billion DNA windows of 4 to 24 characters
      1. ...
      2. ...
   * Search DNA to find DNA 'words'

## Similarity Search Definition ##
   * Given a distance function:
      * `(defn f [a b] "Compute similarity of a and b." ...)`
   * Find the closes elements to a query based on f
   * e.g., 
      * Hamming distance

## DNA Processing ##
   * 10 million objects:
      * 27500 ms => 15 ms with an appropriate data structure in Clojure
   * Scroll a window across a string of DNA and compare each window snapshot against known DNA sequences for different species
   * Extract 'words' from the DNA sequence
   * Process:
      1. ...
      2. Refine ...
      3. Filter clusters by projection 
      4. Rank predictions
      5. Post processing

## Where does Clojure come in? ##
   * Thoughts on Clojure
      * Processing/transforming large files is easy -> partition-by
      * Like a 'think laboratory'
      * Lisp + JVM is a brilliant and powerful combination
         * Expressive
         * JVM environment and libraries
   * Data Processing

## Conclusions ##
   * Discovered part of the genomic code with
      * Clojure + Similarity Search
      * ...
   * Biology is complex
      * Biology easily ...

## Questions ##
   * What did you wish you had in the language?
      * Error messages were a little difficult to understand
      * Now use `{:pre ...}` and `{:post ...}` to help with debugging

