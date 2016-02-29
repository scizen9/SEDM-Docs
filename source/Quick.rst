
Quick Reference for Observers 
=============================

We are in the process of developing an automated system for data reduction and analysis.  Currently, the only interactive step in the data reduction is placing the aperture(s) on the object(s).  For PTF followup, the data are usually taken in A/B pairs to improve the sky subtraction.  This requires that the observer place an aperture on the A position (positive: blue) and on the B position (negative: red).  See below for a step-by-step procedure.  This step may eventually be automated, depending on how robust and accurate our astrometry is.

Once the apertures have been placed, all that remains is to generate an ascii spectrum of the object and then run your favorite classifier.  SNID is provided, but the format is universal enough to be input to any classifier (Superfit, e.g.). The final step is uploading the spectrum and any classification data (type, age, redshift, template figures) to the PTF marshal.  For this, we suggest you use your own account so you are recorded as the observer.


Step-by-step procedure
----------------------

1. Log into sedmdrp@pharos
2. cd into current (UT) date directory:
    * cd /scr2/sedmdrp/redux/20151115 (e.g.)
3. Confirm science targets:
    * grep science Makefile
4. Initiate final reduction of science targets:
    * make science
5. Place aperture(s) on targets (see figs below):
    * confer with PTF marshal cutouts and finder charts for object
    * find A object (positive: blue)
    * place red aperture on target
    * adjust size with 'z' or 'x' keys
    * left click when sized and placed
    * repeat for B object (negative: red)

.. figure:: PTF15drk_AperA.png

    A/B Aperture placement: Aper A goes on positive (blue) target.

.. figure:: PTF15drk_AperB.png

    A/B Aperture placement: Aper B goes on negative (red) target.

6. Generate ascii spectrum and confirm extraction:
    * chspec sp_PTF15drk.npy (e.g.)
    * this will generate :download:`PTF15drk_SEDM.txt`

.. figure:: PTF15drk_SEDM.png

    Extraction of PTF15drk.


7. Run classifier:
    * snid PTF15drk_SEDM.txt
8. Record and upload results to marshal


Data Format & Fields of View
----------------------------


Magnitude Limits
----------------


