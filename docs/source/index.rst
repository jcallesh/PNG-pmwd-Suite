.. _PNG-pmwd Suite:

PNG-pmwd Suite
==============

.. image:: png-pmwd_suite.png
   :width: 500
   :alt: PNG-pmwd Suite logo

Overview
--------

The PNG-pmwd Suite is a collection of :math:`22,410` halo catalogs developed to support data-driven analyses of large-scale structure formation and the impact of primordial non-Gaussianity (PNG).

The suite includes:

- 6 Latin hypercube sets evaluated at redshift :math:`0.5030475235459835`.
- All datasets incorporate non-Gaussian initial conditions.
- Two additional datasets, one corresponding to a fiducial flat :math:`\Lambda` CDM cosmology and 1P design that varies one parameter at a time.
- :math:`22,421` CPU hours used.

The dark matter snapshots were generated using the `Differentiable Cosmological Simulation with the Adjoint Method <https://iopscience.iop.org/article/10.3847/1538-4365/ad0ce7>`_, a fast N-body solver fully differentiable implemented in JAX and freely available at `pmwd code <https://github.com/eelregit/pmwd/tree/master>`_.

Initial conditions are set using second-order Lagrangian displacement (2LPT) at redshift :math:`z=9`, with a linear power spectrum based on the the transfer functions of `Eisenstein & Hu <https://background.uchicago.edu/~whu/transfer/transferpage.html>`_. The linear matter power spectrum for the fiducial cosmology can be found `here <linear_powerspectrum/pmwd_matterpow_0p503.dat>`_.

Each simulation evolves :math:`512^3` dark matter particles in a periodic box of size :math:`(1 Gpc/h)^3` over 20 time steps, reaching the final redshift of :math:`z=0.5030475235459835`.

To implement primordial non-Gaussian initial conditions, we developed a modified version of the code based on the prescription by `Scoccimarro, Hui, Manera, and Chan <https://arxiv.org/abs/1108.5512>`_.

    > The updated codebase with local and equilateral templates can be found at: `pmwd PNG version <https://github.com/jcallesh/pmwd/tree/master>`_.

Each simulation is initialized with a unique random seed, consistently applied across all datasets. Specifically, simulation :math:`i` uses a seed given by :math:`10 \times i + 5`. For example, both 'LH_LC/pmwd_halos_run10.npz' and 'LH_EQ/pmwd_halos_run10.npz' are initialized with a seed value of 105.

The fiducial cosmology and simulation specifications are chosen to closely match the characteristics of the `Quijote simulations <https://arxiv.org/abs/1909.05273>`_, assuming a flat :math:`\Lambda` CDM cosmology with:

    :math:`\Omega_m=0.3175`, :math:`\Omega_b=0.049`, :math:`h=0.6711`, :math:`n_s=0.9624`, :math:`\sigma_8=0.834`, :math:`f_{NL}^{local}=0`, and :math:`f_{NL}^{equil}=0`.  

Halos are identified using a Friends-of-Friends (FoF) algorithm `(Davis, Efstathiou, Frenk, and White) <https://ui.adsabs.harvard.edu/abs/1985ApJ...292..371D>`_ with a linking length of 0.2.
We use the public `nbodykit <https://nbodykit.readthedocs.io/en/latest/index.html>`_ library and store halos containing at least 20 particles.
Dark matter particle snapshots are not stored.

Latin-hypercubes
----------------

The PNG-pmwd Suite explores variations in both primordial non-Gaussiniaties amplitudes and standard cosmological parameters:

- **Primordial Non-Gaussianity**: (:math:`f_{\textrm{NL}}^{\textrm{local}}`:, :math:`f_{\textrm{NL}}^{\textrm{equil}}`)
- **Standard Cosmology**: (:math:`\Omega_m`, :math:`\sigma_8`)


We summarize all the datasets in the following table:

+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
|  Dataset       | :math:`\Omega_m`    | :math:`\sigma_8`            | :math:`f_{\textrm{NL}}^{\textrm{local}}` | :math:`f_{\textrm{NL}}^{\textrm{equil}}` | Realizations |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
|  fiducial      |    0.3175           |            0.834            |                 0                        |              0                           |         2000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_LC300       |    0.3175           |            0.834            |                 [-300,300]               |              0                           |         2000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_LC50        |    0.3175           |            0.834            |                 [-50,50]                 |              0                           |         2000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_EQ600       |    0.3175           |            0.834            |                 0                        |           [-600,600]                     |         2000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_EQ250       |    0.3175           |            0.834            |                 0                        |           [-250,250]                     |         2000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_LC_om_s8    |   [0.2825,0.3525]   |      [0.804, 0.864]         |                 [-50,50]                 |              0                           |         6000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
| LH_EQ_om_s8    |   [0.2825,0.3525]   |      [0.804, 0.864]         |                  0                       |           [-250,250]                     |         6000 |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+
|     1P         |   [0.2825,0.3525]   |      [0.804, 0.864]         |                 [-50,50]                 |           [-250,250]                     |         410  |
+----------------+---------------------+-----------------------------+------------------------------------------+------------------------------------------+--------------+

For the fiducial case, we add :math:`2,000` simulations using the same seeding strategy as the LH set.

In addition, we include a dataset that varies each parameter at a time within the same range as the LH set with linearly sampled steps sizes:
    
    :math:`\Delta\Omega_m:0.007`, :math:`\Delta\sigma_8:0.006`, :math:`\Delta f_{\textrm{NL}}^{\textrm{local}}:10`, and :math:`\Delta f_{\textrm{NL}}^{\textrm{equil}}:50`.

For each parameter, we consider 5 negative and 5 positve steps from the fiducial value, resulting in 10 steps per parameter and 40 configurations in total. For each configuration we include 10 realizations, totaling 400 simulations.
However, the seeding strategey has been shifted by 10000 for realizations 0 to 9.

Total realization count: :math:`22,410` across all datasets. The parameter ranges are centered around the fiducial cosmology in the parameter space.

The values for each parameter set are provided in the corresponding text files named latin_hypercube_params_{dataset}.txt, where {dataset} matches the labels listed in the table.
And 'one_params_steps.txt' contains the values for the 1P dataset. 

The Latin hypercubes values can also be found in `(here) <Latin_hypercube/>`_.


Access to data
--------------

Comming soon.


The Halo Catalogs
------------------

The catalogs can be used in Python with the following script:

.. code-block:: python

    import numpy as np
    fname = 'Halo_catalogs/LH_LC300/pmwd_halos_run0.npz'
    mycat = np.load(fname)

    z      = 0.5030475235459835
    pos_h  = mycat['pos'][:,1:]                   # shape: (3, N_halos) --> X,Y,Z Halo positions in Mpc/h
    vel_h  = (mycat['vel'][:,1:]*100.*(1.+z))     # shape: (3, N_halos) --> Vx, Vy, Vz Halo peculiar velocities in km/s
    np_h   = mycat['np_h'][1:]                    # shape: (N_halos,)   --> Number of particles in each halo
    mass_h = mycat['mass'][1:]                    # shape: (N_halos,)   --> Halo mass in Msun/h

In addition, we provide .json files for each simulation containing detailed metadata, configuration, and cosmology information.
Check the Tutorial notebook `(Tutorial.ipynb) <Tutorial/tutorial.ipynb>`_.

Post-processing data
--------------------

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

We compute the redshift-space halo power spectrum using the public PBI4 tool `(available here) <https://github.com/matteobiagetti/pbi4>`_, , which implements a fourth-order interpolation scheme with interlacing. This method follows the approach detailed in `Sefusatti, Crocce, Scoccimarro, Couchman <https://arxiv.org/abs/1512.07295>`_.

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

Power spectra are in units of :math:`[h/Mpc]^3`.

**bispectrum**

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


Team
----

The PNG-pmwd Suite was developed in 2025 by:

- **Juan Calles** (Universidad de Valparaíso, Chile)
- **Gabriella Contardo** (????)
- **Jorge Noreña** (Pontificia Universidad Católica de Valparaíso, Chile)

Citation
--------

If you use data from the PNG-pmwd Suite, please cite:

`XXXX (2025) <https://arxiv.org/abs/xxxx.xxxxx>`_

.. note::
    Powered@NLHPC: This research was partially supported by the supercomputing infrastructure of the NLHPC (CCSS210001).
