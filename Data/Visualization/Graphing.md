# Graphing

* Forward decay
* T-digest
* HdrHistogram

> Beware that averaging percentiles, e.g., to reduce the time resolution or to combine data from several machines, is mathematically meaningless - the right way of aggregating response time data is to add the histograms.

* [Don't use Timers with exponentially-decaying reservoirs in Graphite](http://taint.org/2014/01/16/145944a.html)