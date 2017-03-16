
Quick Reference for Observers 
=============================

Data Reduction
--------------

See :ref:`this page <SEDM Pipeline>` for documentation on the data reduction
pipeline.


Data Format & Fields of View
----------------------------

Both cameras produce 2048 pixel square images.  The field-of-view of the IFU camera is roughly 30\" on a side, while
the Rainbow Camera (RC) has a field-of-view that is roughly 13\' on a side that is divided into quadrants for each of
the four filters (``ugri``), which have individual FOVs of about 6.5\' on a side.


Exposure Time Estimates
-----------------------

IFU exposure time recommendations for standard stars (single A exposure):

* 10 - 11 mag --> 120s
* 11 - 12 mag --> 240s
* 12 - 13 mag --> 360s
* 13 - 14 mag --> 500s

Exposures longer than this might be considered for an A/B pair.

IFU exposure time (total) recommendations for science targets (split A/B pair):

* 15 mag --> 420s
* 16 mag --> 600s
* 17 mag --> 900s
* 18 mag --> 1800s
* 19 mag --> 2700s
* 20 mag --> 3600s
* 21 mag --> 5400s

Last updated on |version|
