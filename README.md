# node-red-contrib-P2

Background
==========

The **𝗣² algorithm** of Jain and Chlamtec (1985) for dynamic calculation of quantiles without storing observations.

[Communication of the ACM, October 1985, Volume 28, Number 10, Page 1076.](https://dl.acm.org/doi/pdf/10.1145/4372.4378)

A heuristic algorithm for dynamic calculation of the median and other quantiles.
The estimates are produced dynamically as the observations are generated.
The observations are not stored; therefore, the algorithm has a very small and fixed storage requirement regardless of the number of observations.

Installation
============
Download the ....tgz archive and install via node-red-editor menu "manage palette > install > upload button" .


Configuration
=============

**Quantiles** - an array of numbers between 0 and 1, representing the quantiles the node should estimate from the stream of incoming data. 
a single quantile must also be specified as an array: `[0.5]` will estimate the median. 
the three quartils can be configured with `[0.25,0.5,0.75]` for example.


Input
=====

`msg.payload` - number or array of numbers. the algorithm operates on numbers only. array data is processed as separate data streams for every array position.

`msg.topic` - String. different topics are also treated as separate data streams.


Output
======

msg properties are not changed, except

`msg.Quantile` - Object.
 property is added to the message with the resulting estimates for the configured quantile(s).
 if payload was an array on input, msg.Quantile will be the corresponding array of quantiles.

Details
=======

A `msg.reset` (any value) resets the accumulated data for the resp. topic. 
A `msg.reset` without `msg.topic` resets all topics in one go.

Accumulated data is held in the default context store. if the default context store is persistent, so is the accumulated data.

Essential parts of javascript function code created after C++ code of the [GNU Scientific Library](https://www.gnu.org/software/gsl/doc/html/rstat.html#quantiles)
