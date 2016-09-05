
Quick Reference for Observers 
=============================

We are in the process of developing an automated system for data reduction
and analysis.  Currently, the only interactive step in the data reduction
is placing the aperture(s) on the object(s).  For PTF followup, the data
are usually taken in A/B pairs to improve the sky subtraction.  This
requires that the observer place an aperture on the A position (positive:
red) and on the B position (negative: blue).  See below for a step-by-step
procedure.  These steps may eventually be automated, depending on how
robust and accurate our astrometry turns out to be.

Once the apertures have been placed, an ascii spectrum is automatically
generated and all that remains is to run your favorite classifier on the
output spectrum.  SNID is provided, but the format is universal enough to
be input to any classifier (Superfit, e.g.). The final step is uploading
the spectrum and any classification data (type, age, redshift, template
figures) to the PTF marshal.  For this, we suggest you use your own account
so you are recorded as the uploader.


Pre-observing scripted reductions
---------------------------------

Before the observer interacts with the pipeline, the following steps are automatically performed:

#. The appropriate reduced directory is created using the UT date:
    * ``/scr2/sedmdrp/redux/20151115`` (e.g.)
#. The required raw calibration files are copied over and reduced.
#. If there is a failure in the reduction, calibrations files from previous runs are copied.
#. All subsequent ifu images are automatically bias-subtracted, cosmic ray cleaned, and background subtracted.
#. Any subsequent standard star ifu observations are reduced and extracted, and a flux calibration is generated.


Step-by-step procedure
----------------------

The observer connects with pharos either through VNC (recommended), or via an X enabled ssh connection (slower).
Below is is a figure showing the layout of the desktop connected through the VNC connection.

.. figure:: PharosSEDMdesktop.png

    Figure 1. Pharos sedmdrp desktop on screen 7 (5907).

The automatic pipeline script is running in the bottom right window.  Some status information can be gleaned from the
output there.  The xterm set on the left may be used by the observer to examine the files on pharos.  A web browser
will be set up on the desktop screen to the right which can be selected using the chooser on the lower right.  This is
where you can interact with the marshal.

Please be sure that the background subtraction has finished for the target you are reducing.
This is the most time-consuming step.  For each observation it will perform five iterations
of traditional convolution, followed by an iteration of fast-Fourier convolution.  For the
A/B pairs, it will do this twice.  Check the lower-right window to see if the background
subtraction is in process.

In the top-right Xterm window, the observer interacts with the pipeline using the following steps:

1. cd into current (UT) date directory:
    * ``cd /scr2/sedmdrp/redux/20151115`` (e.g.)
2. Confirm science targets:
    * ``grep science Makefile``
    * A/B pairs will have target names like ``PTF15drk.npy``
    * if the pair has not finished the target name will be something like ``PTF15drk_obs1_0.npy``
    * do not process partial A/B pairs unless one has failed: the sky subtraction will be inferior
3. Initiate final reduction of science targets:
    * ``make science``  --> to make all science targets or
    * ``make PTF15drk.npy`` --> to make a specific target (e.g.)
    * Note: targets that are already processed will not be re-done, so ``make science`` is a reasonable step after each pair has been read out.
4. Scale the data cube:
    * Use '>' and '<' keys to adjust the A/B cube scaling limits until good visibility is obtained.
    * Hit 'x' to use new scale or 'q' to abandon adjustments and revert to default scaling.

.. figure:: PTF15drk_Scale.png

    Figure 2. Scaling the data cube for good visibility of targets.

5. Place aperture on A target:
    * confer with `PTF marshal`__ cutouts and finder charts for the `target object`__ (e.g.)
    * find A object (positive: red)
    * place red aperture on target
    * adjust size with 'z' or 'x' keys
    * sky subtraction can be toggled on/off with the 'y' key (normally on)
    * left click when sized and placed

__ http://ptf.caltech.edu/cgi-bin/ptf/transient/marshal.cgi
__ http://ptf.caltech.edu/cgi-bin/ptf/transient/view_source.cgi?name=15drk

.. figure:: PTF15drk_AperA.png

    Figure 3. A/B Aperture placement: Aper A goes on positive (red) target.

6. Place aperture on B target:
    * If A/B pair, find B object (negative: blue)
    * place red aperture on target
    * adjust size with 'z' or 'x' keys (should be same size as A)
    * left click when sized and placed

.. figure:: PTF15drk_AperB.png

    Figure 4. A/B Aperture placement: Aper B goes on negative (blue) target.

7. When prompted, enter quality of observation as follows:
    * 1 - good         (no problems)
    * 2 - acceptable   (minor problems)
    * 3 - poor         (major problems)
    * 4 - no object visible
    * (Only quality 1 and 2 will be uploaded to the marshal)

8. Completing step 7 will automatically generate an ascii spectrum and a pdf plot:
    * The ascii spectrum (e.g, :download:`PTF15drk_SEDM.txt`)
    * The pdf plot (e.g, :download:`PTF15drk_SEDM.pdf`, see plot below)
    * display the pdf with ``evince PTF15drk_SEDM.pdf`` (e.g.)

.. figure:: PTF15drk_SEDM.png

    Figure 5. Extracted spectrum plot of PTF15drk.

9. Redo an object.  If you wish to redo an object because of improper aperture placement, or for any other reason simply type:
    * ``make redo_PTF15drk`` (e.g., for A/B pair)
    * ``make redo_PTF15drk_obs1_0`` (e.g., for a single-frame observation)
10. You can then re-place the aperture and remake the extracted spectrum by typing
     * ``make science`` or
     * ``make sp_PTF15drk.npy`` (e.g.)
     * Using the science target is recommended.
11. If you typed ``make science`` to initiate the data reduction,
    then an ascii report on the reductions is generated in the file
    ``report.txt``.
12. Most results and diagnostic plots are now automatically copied to the
    UT date subdirectory on the documentation web server in the directory
    `linked here`_.  Consult this page to check aperture placement, etc.

.. _linked here: http://www.astro.caltech.edu/sedm/redux/

13. When the night is complete, we now use an automatic script to upload the
    resulting spectra to the marshal.  To generate an e-mail report on the entire
    night of data reductions and initiate the automatic upload of the resulting
    spectra to the marshal, please enter:
     * ``make finalreport``



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
