
Efficiency
==========

It is important to calculate the efficiency of the final spectral extraction
from the SEDM pipeline.  This is done by comparing the expected standard
star flux with the observed standard star flux.  Although that sounds easy,
in practice there are many pitfalls to this calculation.  This page documents
the process by which we derive the efficiency.


Standard Flux
-------------

The reference data used for this exercise is a tabulated list of fluxes for
a given standard star.  In our case these are in units of
:math:`F_{\lambda,ref} = erg\ s^{-1} cm^{-2} A^{-1}`.
Since CCDs measure the number of photons observed, our first task is to
convert this flux unit into
:math:`F_{ph,ref} = photons\ s^{-1} cm^{-2} A^{-1}`.

We know that the energy of a photon is :math:`E_{ph}(\lambda) = h\nu = hc/\lambda`.  The
wavelength dependency must be accounted for when converting to photon flux.
Planck's constant is :math:`h = 6.62606885\times 10^{-27} erg\ s` which,
when multiplied by the speed of light in Angstroms/s gives
:math:`hc = 1.98782\times 10^{-8} erg\ A`.  Thus we get a conversion to
photon flux of :math:`F_{ph,ref} = \frac{F_{\lambda,ref}}{E_{ph}(\lambda)} = \frac{erg\ s^{-1} cm^{-2} A^{-1}}{\frac{1.98782\times 10^{-8} erg\ A}{\lambda}}`.
This gives a final conversion of
:math:`F_{ph,ref} = F_{\lambda,ref} * 5.034\times 10^7 * \lambda`, in units of
:math:`photons\ s^{-1} cm^{-2} A^{-1}`.


Observed Flux
-------------

While the previous calculation is pretty basic, calculating the observed
spectrum is where many pitfalls are encountered.  In particular, since our
standard flux is now in :math:`photons\ s^{-1} cm^{-2} A^{-1}` and it is
very unlikely that the native wavelength bins of our observations are all
1 Angstrom wide, we must carefully account for the native size of the 
wavelength sampling.  To do this, we must use the wavelength scale that is
most representative of the cube's geometry solution.  For the SEDM, this is
currently derived from the central five arcseconds of the IFU field of view.
This avoids any edge effects and should represent the region where most of
the standard stars are observed.

Previously we used a fiducial wavelength scale derived from an analytic
function that roughly approximated the run of wavelengths for SEDM.  However,
it is important for this calculation that a wavelength scale as close to the
native scale as possible is used.  Therefore, we switched to using an average
scale derived from the central five arcseconds.  This changed the shape of the
efficiency curve and made it more accurate.

We show the two wavelength scales below in the figure.

Next we must calculate the size of the wavelength bins, given as
:math:`\Delta\lambda(\lambda)`.

Our observed flux is given as
:math:`F_{ph,obs} = photons\ s^{-1}\ \Delta\lambda(\lambda)^{-1}`.

Now we can calculate the effective area of our instrument using the following
formula:
:math:`A_{eff} = F_{ph,obs} / (F_{ph} * \Delta\lambda(\lambda))`, which has
the units of :math:`cm^2`.  We compare this area to the actual area of the
telescope, corrected for reflective losses to derive the efficiency.



Last updated on |version|
