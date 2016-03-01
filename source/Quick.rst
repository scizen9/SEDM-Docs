
Quick Reference for Observers 
=============================

We are in the process of developing an automated system for data reduction and analysis.  Currently, the only interactive step in the data reduction is placing the aperture(s) on the object(s).  For PTF followup, the data are usually taken in A/B pairs to improve the sky subtraction.  This requires that the observer place an aperture on the A position (positive: blue) and on the B position (negative: red).  See below for a step-by-step procedure.  These steps may eventually be automated, depending on how robust and accurate our astrometry turns out to be.

Once the apertures have been placed, all that remains is to generate an ascii spectrum of the object and then run your favorite classifier.  SNID is provided, but the format is universal enough to be input to any classifier (Superfit, e.g.). The final step is uploading the spectrum and any classification data (type, age, redshift, template figures) to the PTF marshal.  For this, we suggest you use your own account so you are recorded as the observer.


Pre-observing scripted reductions
---------------------------------

Before the observer interacts with the pipeline, the following steps are automatically performed:

#. The appropriate reduced directory is created using the UT date:
    * ``/scr2/sedmdrp/redux/20151115`` (e.g.)
#. The required raw calibration files are copied over and reduced
#. If there is a failure in the reduction, calibrations files from previous runs are copied
#. All subsequent ifu images are automatically bias-subtracted and cosmic ray cleaned.
#. Any subsequent standard star ifu observations are reduced and extracted, and a flux calibration is generated


Step-by-step procedure
----------------------

The observer connects with pharos either through VNC (recommended), or via an X enabled ssh connection (slower).  Then the observer-pipeline interaction proceeds with the following steps:

1. cd into current (UT) date directory:
    * ``cd /scr2/sedmdrp/redux/20151115`` (e.g.)
2. Confirm science targets:
    * ``grep science Makefile``
3. Initiate final reduction of science targets:
    * ``make science``
4. Place aperture on A target:
    * confer with PTF marshal cutouts and finder charts for object
    * find A object (positive: blue)
    * place red aperture on target
    * adjust size with 'z' or 'x' keys
    * left click when sized and placed

.. figure:: PTF15drk_AperA.png

    A/B Aperture placement: Aper A goes on positive (blue) target.

5. Place aperture on B target:
    * If A/B pair, find B object (negative: red)
    * place red aperture on target
    * adjust size with 'z' or 'x' keys (should be same size as A)
    * left click when sized and placed

.. figure:: PTF15drk_AperB.png

    A/B Aperture placement: Aper B goes on negative (red) target.

6. Generate ascii spectrum and confirm extraction:
    * ``chspec sp_PTF15drk.npy`` (e.g.)
    * this will generate :download:`PTF15drk_SEDM.txt`

.. figure:: PTF15drk_SEDM.png

    Extracted spectrum plot of PTF15drk. Close this window to generate PTF15drk_SEDM.txt

7. Run classifier:
    * ``snid PTF15drk_SEDM.txt`` (e.g.)
    * convert ps output to png:
         * ``ps2png <snid_output>.ps <outfile>.png``

8. Record and upload results (type, age, redshift, template plots) to marshal.


Data Format & Fields of View
----------------------------

Both cameras produce 2048 pixel square images.  The field-of-view of the IFU camera is roughly 30 arcsec on a side, while the Rainbow Camera has a field-of-view that is roughly 13 arcmin on a side.


Magnitude Limits
----------------


