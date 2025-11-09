.. _post-processing-data:

********************
Post-processing data
********************

We provide the following post-processed measurements derived from each simulation in the PNG-pmwd Suite:

- Halo-Halo Power spectrum.
- Halo-Halo-Halo Bispectrum.
- Others?

All measurements are performed in redshift space. To mimic observational data, we apply the distant-observer approximation, shifting halo positions along the line of sight (assumed to be the z-axis). The shift accounts for the halo's peculiar velocity and the cosmological Hubble expansion, using the appropriate scale factor and cosmological parameters of each catalog.

The redshift-space displacement is given by:

:math:`\boldsymbol{x}_{\text{rs}} = \boldsymbol{x} + \frac{\boldsymbol{v} \cdot \hat{\boldsymbol{z}}}{a(z) H(z)} \hat{\boldsymbol{z}}`

Where:

- :math:`\boldsymbol{x}` is the halo's real-space position
- :math:`\boldsymbol{v}` is the peculiar velocity
- :math:`a(z) = (1 + z)^{-1}` is the scale factor
- The Hubble parameter is assumed to be in perfect matter domination era given by:

.. math::

   H(z) = 100 \sqrt{\Omega_{m} a^{-3} + \Omega_{\Lambda} }

expressed in :math:`(km/s)(h/Mpc)`, and evaluated using each simulation's cosmology.

**Power spectrum**

We compute the redshift-space halo power spectrum using the public PBI4 tool `(available here) <https://github.com/matteobiagetti/pbi4>`_, which implements a fourth-order interpolation scheme with interlacing. This method follows the approach detailed in `Sefusatti, Crocce, Scoccimarro, Couchman <https://arxiv.org/abs/1512.07295>`_.

Power spectrum measurements are binned using a spacing of :math:`\Delta k = 2k_f`, where the fundamental mode is defined by the box size as :math:`k_f \approx 0.006 [h/Mpc]`. The analysis includes modes up to :math:`k_{max} \approx 0.45 [h/Mpc]` in :math:`36` bins.

Each power spectrum file can be read in Python as follows,

.. code-block:: python

    import numpy as np
    filename = 'powerspectrum_hh_pmwd_irsd3_LC_mbin0_run1_grid144_z0p503.dat'
    k, avgk, P0PSN, P2,  P4, Nmodes, PSN = np.loadtxt(filename, unpack=True)
    P0 = P0PSN - PSN #Shot noise subtracted monopole

where:

- :math:`k` is the wavenumber bin center in units of :math:`[h/Mpc]`.
- :math:`k_{avg}` is the average wavenumber in the bin.
- :math:`P0PSN: P^{\ell=0}+PSN`, :math:`P2: P^{\ell=2}(k)`, and :math:`P4: P^{\ell=4}(k)` are the monopole, quadrupole, and hexadecapole moments.
- :math:`PSN` is the Poisson shot noise.

Power spectra are in units of :math:`[h/Mpc]^3`. Check the Tutorial notebook `Powerspectrum <Tutorial/Powerspectrum.html>`_.

**Bispectrum**

Using the same k-bin definitions as in the power spectrum analysis, we also compute the redshift-space bispectrum for each halo catalog. The bispectrum includes :math:`1522` triangle configurations formed by triplets of wavevectors with :math:`k_i \leq 0.3 [h/Mpc]`.

Each bispectrum file can be read in Python as follows

.. code-block:: python

    import numpy as np
    filename = 'bispectrum_hhh_pmwd_irsd3_LC_mbin0_run1_grid144_z0p503.dat'
    k1, k2, k3, Pk1, Pk2, Pk3, B0BSN, BSN, N_tr, B2, B4 = np.loadtxt(filename, unpack=True)
    B0 = B0BSN - BSN #Shot noise subtracted B0

Where:

- :math:`k_1, k_2, k_3` are the wavenumbers of the triangle sides in units of the fundamental frequency :math:`k_f`.
- :math:`B0BSN = B(k_1,k_2,k_3)` is the measured bispectrum :math:`[h/Mpc]^6`; includes the shot-noise contribution.
- BSN is the shot-noise correction computed as:
    :math:`BSN = \frac{1}{n^2} + \frac{P(k_1) + P(k_2) + P(k_3)}{n}`
    where :math:`n` is the halo number density.
- :math:`N_{tr}` is the number of triangles in the bin
- :math:`B2` and :math:`B4` are the bispectrum quadrupole and hexadecapole moments, respectively.

Check the Tutorial notebook `Bispectrum <Tutorial/Bispectrum.html>`_.
