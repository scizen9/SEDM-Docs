.. SED Machine documentation master file, created by
   sphinx-quickstart on Sun Jun  7 12:15:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to SED Machine's documentation!
=======================================

The SED Machine is very low resolution (:math:`\frac{\lambda}{\Delta
\lambda}\sim100`) optical (365 - 1,000 nm) integral field (30"x"30")
spectrograph and a rainbow imager with a 13' x 13' field. The rainbow
camera images are partitioned into u, g, r, and i bands, each with a 6' x
6' field of view. The instrument was designed for rapid classification of
supernovae from transient surveys. To achieve this goal, the instrument was
designed to have:

- Low resolution (:math:`R=\frac{\lambda}{\Delta \lambda}\sim100`), sufficient for classification.
- High "Slit to detector" photon throughput.
- 0.1 mag precision spectrophotometry.

The hardware project was funded by the NSF with a grant to Caltech.  Many
people were involved.  Current members of the team are:

- Michael Feeney (Instrument Master)
- Richard Walters (Telescope/Instrument Operations and Scheduling)
- Don Neill (Commissioning Scientist, IFU pipeline)
- Nadejda Blagorodnova (Science results, RCam photometry pipeline)
- Mickael Rigault (IFU pipeline lead developper, CNRS/IN2P3, France)
- Chris Cannella (Marshal interface, ATels)
- Jamey Eriksen (Operations Support at Palomar)
- Jeff Zolkower (Operations Support at Palomar)

Former members, some of whom are still consulted for advice are:

- Nick Konidaris (Principle Investigator)
- Robert Quimby (Project Scientist)
- Jack Davis, and Sagi Ben-Ami (Weizmann institute grad students)
- Karl Vyhmeister (SEDM Database)

Here we document the instrument for observers and developers.  Observers
will want to refer to the Observer's Reference below.

Data products produced by the automatic pipeline can be found `here`_.

.. _here: http://www.astro.caltech.edu/sedm/redux/?C=N;O=D



Contents:

.. toctree::
    :numbered:
    :maxdepth: 2

    Introduction
    ObsRef
    Pipeline
    Efficiency
    Hardware
    Components
    Old_Pipeline

Last updated on |version|
