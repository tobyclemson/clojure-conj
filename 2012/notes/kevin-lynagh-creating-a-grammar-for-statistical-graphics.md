## "Creating a Grammar for Statistical Graphics", Kevin Lynagh #

## Data Visualisation: What, Why and How ##
* Wind energy
  * iPad app for wind farms
  * Infrastructure existed to collect data about generators in a wind farm
  * Data stored in a database
  * Not much being done with it
* Bioinformatics: EdgeBio
  * Dashboard for gene sequencing data
* Orbitz vs. Hipmunk
  * Using visual representation to make the data easier to consume

### How (Theory) ###
* Mapping from data to visual aesthetics
* Map data to:
  * length of a line
  * width
  * orientation
  * intensity
  * size
  * shape
  * enclosure
  * 2 dimensional position
* Some aesthetics are better than others
  * 2D position/length > width > size
  * For example, pie charts aren't the best representation, if you
    take the numbers away it's very hard to read
* Have a thesis

### How (Practice) ###
* Off the rack (specific)
  * Microsoft Excel
  * Adobe Illustrator
* Bespoke (general)
  * D3: Data Driven Documents
  * Takes a lot of work to put together the visualisations
* General (hard to use) ----?---> Specific (not expressive)  
  
## A Grammar of Graphics ##
* Actually a book by Leland Wilkinson
* ggplot2 partially implements the grammar in R
* Example: motor trend cars dataset
* ggplot(...)
* Written in R
* Wouldn't it be nice to have it in Clojure
* Existing grammar is very complected, tied together into a single
  function for a particular visualisation
* Decomplect: a graphic consists of
  * Data
  * Geometry
  * Aesthetic
  * Mappings
  * Statistics
  * Groupings
  * Scales
* `{:data mtcars
    :geom #point{:radius 4}
    :mapping {:y :mpg :x :wt}}`
* `#type{...}`: typed literal
* But the complete expression must include more
* What you want is to express just the piece you care about and have
  it convert to the full form
* Pattern rewrites
* core.logic?
  * My program would be so much better in core.logic...if only I knew how
  * Rewrite idea came from kibit by Jonas Enlund
* Data all the things
  * API support
* Spec --> Plot --> SVG/PDF/PNG
* Plot is just a map, you can intercept the rending and reprocess
* A grammar lets you say lots of things
