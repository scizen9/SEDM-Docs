
Efficiency for KPY pipeline
===========================

It is important to calculate the efficiency of the final spectral
extraction from the SEDM pipeline.  This is done by comparing the expected
standard star flux with the observed standard star flux.  Although that
sounds easy, in practice there are many pitfalls to this calculation.  This
page documents the process by which we derive the efficiency.

At this time it is important to acknowledge the efforts of Jason Fucik,
Rich Dekany, and David Hover in producing the models of the SEDM optical
system and in performing lab measurements and analysis.  In particular,
Jason made the crucial discovery of the low throughput 'smoking gun' and is
leading the acquisition of an improved micro-lens array.


Standard Flux
-------------

The reference data used for this calculation is a tabulated list of fluxes
for a given standard star.  In our case these are in units of
:math:`F_{\lambda,ref} = erg\ s^{-1} cm^{-2} A^{-1}`.  Since CCDs measure
the number of photons observed, our first task is to convert this energy
flux into photon (:math:`e^-`) flux, :math:`F_{ph,ref} = e^-\ s^{-1}
cm^{-2} A^{-1}`.

We know the energy of a photon is :math:`E_{ph}(\lambda) = hc/\lambda\ erg/
e^-`.  The wavelength dependency must be accounted for when converting to
photon flux.  Planck's constant is :math:`h = 6.62606885\times 10^{-27}
erg\ s` which, when multiplied by the speed of light in :math:`A\ s^{-1}`
gives :math:`hc = 1.98782\times 10^{-8} erg\ A`.  Thus, we get a conversion
to photon flux of :math:`F_{ph,ref} =
\frac{F_{\lambda,ref}}{E_{ph}(\lambda)} = \frac{erg\ s^{-1} cm^{-2} A^{-1}\
e^-}{1.98782\times 10^{-8} erg\ A}\lambda\ A`.  This gives a final
conversion of :math:`F_{ph,ref} = 5.034\times 10^7 F_{\lambda,ref}
\lambda`, in units of :math:`e^-\ s^{-1} cm^{-2} A^{-1}`.


Observed Flux
-------------

While the previous calculation is pretty basic, calculating the observed
spectrum is where many pitfalls are encountered.  In particular, since our
standard flux is now in :math:`e^-\ s^{-1} cm^{-2} A^{-1}` and it is very
unlikely that the native wavelength bins of our observations are all 1
Angstrom wide, we must carefully account for the native size of the
wavelength sampling.  To do this, we must use the wavelength scale that is
most representative of the cube's geometry solution.

It is also important that we collect as much of the standard star's light
from the raw image as possible.  This means using a large number of
spaxels, which makes our calculation more susceptible to background
problems.  Because of this, we derive our fiducial wavelength scale from
the central five arcseconds of the IFU field of view.  This avoids any edge
effects and should represent the region where most of the standard stars
are observed.

In addition, all observations of standard stars are corrected for
atmospheric extinction using the standard extinction curves for Palomar
(Hayes & Latham 1975).


Wavelength Scale
^^^^^^^^^^^^^^^^

Previously we used a function :math:`(\lambda(x) = 1050(239/240)^x, x: 0 -
265)` for the fiducial wavelength scale that roughly approximates the run
of wavelengths for SEDM.  However, it is important for this calculation
that the wavelength scale be as close to the native scale as possible.
Therefore, we switched to using an average scale derived from spaxels in
the central five arcseconds of the IFU.  This changed the shape of the
efficiency curve and made it more accurate.


.. _fig-waves:

.. figure:: Waves.png

    SEDM old and new fiducial wavelength scales.


Wavelength Bins
^^^^^^^^^^^^^^^

Next we must calculate the size of the wavelength bins, given as
:math:`\Delta\lambda(\lambda)`.  Most spectrographs have a native
wavelength bin size that is approximately constant, which is another way of
saying the dispersion is fairly constant.  Since the SEDM was designed not
to have a constant dispersion, but to have a constant resolution of
:math:`R = \lambda/\Delta\lambda \approx 100`, the dispersion varies
substantially over the wavelength range.  Thus, our wavelength bins are a
function of wavelength, as shown below.

.. _fig-delta_waves:

.. figure:: Delta_Waves.png

    SEDM old and new wavelength bins.


The difference between the average and the function-generated wavelength
scales becomes more pronounced when you use them to calculate the
wavelength bins.  This was the main reason we chose to use an average
wavelength scale rather than a functional form.  Thus, our observed flux is
:math:`F_{ph,obs} = e^-\ s^{-1}\ \Delta\lambda(\lambda)^{-1}`, where
:math:`\Delta\lambda(\lambda)` is given by the average wavelength bins.


Effective Area
--------------

Now we can calculate the effective area of our instrument using the
following formula: :math:`A_{inst,eff}(\lambda) = F_{ph,obs} / (F_{ph,ref}
\Delta\lambda(\lambda))`.  All units cancel (see previous formulae) except
:math:`cm^2`, giving what is called the effective area of the instrument as
a function of wavelength.


Efficiency Ratio
----------------

We can now compare this area to the actual area of the telescope, corrected
for reflective losses to derive the efficiency, using this formula:
:math:`T_{inst}(\lambda) = A_{inst,eff}(\lambda)/A_{tel,eff}`.

For reflective losses of the P60 telescope, we have two mirrors, the
primary and secondary, that contribute.  If we assume an average of 91%
reflectivity for the primary (from reflectometer measurements after the
September 2017 re-aluminization) and somewhat less for the secondary which
has not yet been re-aluminized, say 90%, we get the total reflective
throughput of 82%.  We then use the area of the primary mirror, accounting
for the secondary obstruction, or :math:`A_{tel} = 18,000\ cm^2`.
Multiplying the reflective througput times the telescope area gives a
telescope effective area of :math:`A_{tel,eff} = 14,742\ cm^2`.  This is
what we divide our instrumental effective area curve by to get the
instrumental throughput.

Below is the figure that shows a typical efficiency curve using our best
understanding of the calculation and of the instrumental wavelength bins.
The efficiency is only as good as the quality of the night and represents an
approximation of the true efficiency.  Clouds will tend to lower the
measured efficiency, but moonlight or other sources of anomolous background
will tend to raise the measured efficiency.  In general, clouds are a more
common source of efficiency offset and so most measurements are lower
limits on the true efficiency.



.. _fig-efficiency:

.. figure:: TypicalEff.png

    Typical SEDM efficiency curve from 2017 Sep. 20 using BD+28d4211.


Importance of Wavelength Bins
-----------------------------

To visualize how the efficiency is calculated, we can think of the
instrument as having buckets to collect photons that correspond to the CCD
pixels.  The dispersive elements of the instrument define what the
wavelength 'size' of each bucket is, while the spatial 'size' of each
bucket is determined by the optical properties of the entire system
(telescope + instrument).  The efficiency is simply the number of photons
we actually collected in our bucket divided by the number of photons we
expect a given bucket to collect.  The number of photons we expect to
collect is obviously a strong function of the size of the bucket; the
bigger the bucket the more photons we expect to collect.  If we assume our
buckets are smaller than they really are, our expectations are
correspondingly low and we get a higher efficiency.  The plot below shows
the result of our initial efficiency calculation, assuming that all of our
buckets are 1 nm in wavelength.  


.. _fig-eff_nodw:

.. figure:: NoDeltaWaveEff.png

    SEDM efficiency assuming our wavelength bins are all 1 nm in size
    (wrong!).


The shape of this curve shows a strong blue linear trend, which is contrary
to the expected curve based on the optical design, ray-traced in ZMAX (see
:ref:`gray curve in figure six below <fig-lab_eff>`).  Once we discovered
that we were not accounting for the wavelength bin size, we re-calculated
the efficiency and since our wavelength bins were not 1 nm, but instead
ranged from approximately 1.5 to 4.5 nm (:ref:`green curve in figure two
<fig-delta_waves>`), the overall efficiency dropped considerably.  The
shape seems to be closer to what is :ref:`expected based on ray-tracing
<fig-lab_eff>`.  However, here we are still using the functional form for our
fiducial wavelengths.  The plot below shows how the overall efficiency
dropped significantly, but because the wavelength bins now vary in size
much closer to the native bin sizes, the shape changed to a more expected
form.


.. _fig-eff_oldfid:

.. figure:: OldFidWaveEff.png

    SEDM efficiency accounting for wavelength bins, but using the old
    fiducial wavelengths (better, but still wrong!).


If we examine the native wavelength solution we find that, in fact, the
wavelength bins range from 1.5 to 5.7 nm (:ref:`blue curve in figure two
<fig-delta_waves>`) and have a trend that differs from that generated using
the functional form.  Compare the figure above with the :ref:`first
efficiency curve <fig-efficiency>` and you will see that at 500 nm, the
efficiency increases by 0.5%, but the peak efficiency goes down.  If you
compare the green and blue curves in :ref:`figure two above
<fig-delta_waves>`, you can see that the largest differences occur around
pixel zero and pixel 200.  Referring to :ref:`figure one above
<fig-waves>`, it is apparent that this changes the shape of the curve
primarily at the red and blue 'shoulders'.


Ray Tracing and Lab Measurements
--------------------------------

While the SEDM was in the lab, from March through August 2017, we were able
to do some analysis of the instrument using a monochrometer and to analyze
a ZMAX model of the optics.  Below is a figure showing some of the results
that we can compare with our on-sky measurements.


.. _fig-lab_eff:

.. figure:: SEDM_efficiency.png
    
    Lab measurements of SEDM throughput (red, blue) compared with the
    ray-traced throughput for a single spaxel (gray), the on-sky throughput
    measured without accounting correctly for wavelength bin size (yellow),
    and the throughput of the instrument without the lenslet array (green).


The yellow curve was derived the same way that :ref:`figure four
<fig-eff_nodw>` was calculated.  Our best calculation shown in :ref:`figure
three <fig-efficiency>` has a shape closer to the gray curve, but with a
lower peak throughput by a factor of more than six.  We point out that the
gray curve is calculated for a single spaxel ray and does not account for
losses due to the lenslet filling factor or dead zones between lenses.  It
is puzzling that our initial (and incorrect) calculation agrees so well
with the lab throughput measurements shown by the red and blue curves.  It
is possible that there is still some accounting for wavelength bins in the
lab measurements that needs to be done.


The Effect of Filling Factor on Efficiency
------------------------------------------

In our efforts to understand the low throughput of the current SEDM, we
have tried to estimate the filling factor of the multi-lens array (MLA).
In the manufacturing process for any MLA, a certain fraction of the array
becomes unusable because of dead zones at the borders of the lenslets.  In
our analysis, we have found that it is crucial to keep these dead zones as
small as possible because, not only do they represent a loss of light, but
they are also a source of scattered light.  The specification for the
orignal MLA was to have a filling factor of around 95%.  Our investigations
have revealed that, due to a :ref:`misalignment of the front and back
lenses <fig-mla_offset>` in the MLA, the effective filling factor is
actually closer to 80%.


.. _fig-mla_offset:

.. figure:: SEDM_MLA_offset.png
    
    Microscopic view of the SEDM MLA with the red color being the front
    surface and the blue color being the back surface.  The dead zones are
    apparent as the dark areas and are exacerbated by the obvious
    mis-alignment of the front and back lenslets.


The impact of this low filling factor is rather extreme and may completely
explain the low instrumental throughput.  The filling factor enters the
throughput calculation as a factor to the power of the number of spaxels
involved, :math:`T_{inst} = T_{spax} \times f_{fill}^{N_{spax}}`.  Using the
peak throughput predicted for a single spaxel (the grey curve in :ref:`the
lab measures figure <fig-lab_eff>`) of 45%, a filling factor of 80%, and
assuming we cover seven spaxels, we get :math:`T_{inst} = 0.45 \times
0.80^{7} = 0.09`, which is very close to the measured throughput peak in
the figure above of our :ref:`best efficiency calculation
<fig-efficiency>`.  The remaining difference is likely due to the fact that
our standard stars usually cover more than seven spaxels and thus the
impact of the filling factor would be greater.

The impact of filling factor is also illustrated by the :ref:`figure below
<fig-filling_factor>`.


.. _fig-filling_factor:

.. figure:: SEDM_filling_factor.png

    The impact of various filling factors on the efficiency curve.  The
    black curve is the predicted throughput based on the ZMAX model, while
    the other colors represent different filling factors as indicated in the
    figure legend.


Good News
^^^^^^^^^

Ultimately, this is good news for the prospect of improving the SEDM
throughput.  In particular, we can avoid the whole issue of alignment by
making the MLA plano-convex instead of double convex.  This should result
in a filling factor much closer to 100% and thus our throughput should jump
by nearly a factor of seven.  We have indeed redesigned the MLA to be
plano-convex and are working with a vendor with the goal of producing a MLA
with a filling factor of 98% (light blue curve in :ref:`the figure above
<fig-filling_factor>`) as a replacement MLA for SEDM (and for any future
versions of the SEDM).


Efficiency Trend
----------------

As stated above, the quality of the night most typically reduces the
efficiency measurement due to atmospheric extinction (clouds), but can also
increase the efficiency if there is a high background (moon).  The best way
to mitigate these effects is to look at the trend over time.  Below is a
figure that shows the efficiency in wavlength bins over the course of the
last 700 days.  This was calculated after re-processing all the archival
data with the average fiducial wavelength scale.

.. _fig-eff_trend:

.. figure:: SEDM_eff_trend.png

    SEDM efficiency in 100 nm bins from 400 to 900 nm over the active
    period of SEDM observations.

Several features of this plot stand out.  There are short periods of higher
efficiency that go against the general trend.  These are most likely from
observations of standard stars that have a high background due to
moonlight.

The other feature is the increase in efficiency to a peak near JD 2457640
and then a general decline.  It's hard to understand the rise in this
trend, while the decline is expected as the mirror coatings deteriorate.
There was a lot of experimentation with the instrument configuration during
the early days, although this would better explain jumps in efficiency and
not a slow general trend.

We also see that the current efficiency is slightly lower than the peak
from the previous group.  If somehow the trend that was seen in the
previous 300 days hold for the next 300, then we should increase to a
similar if not higher peak.


Last updated on |version|
