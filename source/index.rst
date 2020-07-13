.. SED Machine documentation master file, created by
   sphinx-quickstart on Sun Jun  7 12:15:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to SED Machine's documentation!
=======================================

The SED Machine is very low resolution (:math:`\frac{\lambda}{\Delta
\lambda}\sim100`) optical (365 - 1,000 nm) integral field (28"x"28")
spectrograph and a rainbow imager with a 13' x 13' field. The rainbow
camera images are partitioned into u, g, r, and i bands, each with a 6' x
6' field of view. The instrument was designed for rapid classification of
supernovae from transient surveys. To achieve this goal, the instrument was
designed to have:

- Low resolution (:math:`R=\frac{\lambda}{\Delta \lambda}\sim100`), sufficient for classification.
- High "Slit to detector" photon throughput.
- 0.1 mag precision spectrophotometry.

The hardware project was funded by the NSF with a grant to Caltech.  If you use
SEDM data please use the following text in your published papers:

*The SED Machine is based upon work supported by the National Science Foundation under Grant No. 1106171.*

Please also cite our paper on SEDM: `Blagoradnova, Neill, Walters, et al. 2018, PASP, v130, 035003 <https://ui.adsabs.harvard.edu/#abs/2018PASP..130c5003B/abstract>`_.

And if you use IFU data please cite: `Rigault, Neill, Walters, et al. 2019, A&A, 627, A115 <https://ui.adsabs.harvard.edu/abs/2019A%26A...627A.115R/abstract>`_.

Many people were involved.  Current members of the team are:

- Richard Walters (Telescope/Instrument Operations and Scheduling, Caltech)
- Don Neill (Commissioning Scientist, IFU pipeline automation, Caltech)
- Mickael Rigault (IFU pipeline lead developer, CNRS/IN2P3, France)
- Reed Riddle (SEDM-KP software/operations)
- Yashvi Sharma (Caltech grad student)
- Jeff Zolkower (Operations Support, Palomar)
- Nick Ganciu (Operations Support, Palomar)

Former members, some of whom are still consulted for advice are:

- Nick Konidaris (Principle Investigator)
- Robert Quimby (Project Scientist)
- Jack Davis, and Sagi Ben-Ami (Weizmann institute grad students)
- Nadejda Blagorodnova (now at Radboud Univ.)
- Alison Dugas (now at Univ. Hawaii)
- Karl Vyhmeister (SEDM Database)
- Chris Cannella (Marshal interface, ATels)
- Michael Feeney (Instrument Master, now at Amazon)
- Jamey Eriksen (Operations Support, now in Arizona)

Here we document the instrument for observers and developers.  Observers
will want to refer to the Observer's Reference below.

Data products produced by the automatic pipeline can be found `here`_ (a
login account is required).

.. _here: http://pharos.caltech.edu/data_access/ifu



Contents:

.. toctree::
    :numbered:
    :maxdepth: 2

    Introduction
    ObsRef
    Pipeline
    Efficiency
    Timeline
    Hardware
    Components
    Old_Pipeline

Last updated on |version|
