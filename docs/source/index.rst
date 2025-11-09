.. _PNG-pmwd Suite:

PNG-pmwd Suite
==============

.. image:: png-pmwd_suite.png
   :width: 500
   :alt: PNG-pmwd Suite logo

The PNG-pmwd Suite is a collection of :math:`22{,}410` halo catalogs developed to support data-driven analyses of large-scale structure formation and the impact of primordial non-Gaussianity (PNG).

The suite includes:

- 6 Latin hypercube sets evaluated at redshift :math:`0.5030475235459835`.
- All datasets incorporate non-Gaussian initial conditions.
- Two additional datasets, one corresponding to a fiducial flat :math:`\Lambda` CDM cosmology and 1P design that varies one parameter at a time.
- :math:`22{,}421` CPU hours used.

The dark matter snapshots were generated using the `Differentiable Cosmological Simulation with the Adjoint Method <https://iopscience.iop.org/article/10.3847/1538-4365/ad0ce7>`_, a fast N-body solver fully differentiable implemented in JAX and freely available at `pmwd code <https://github.com/eelregit/pmwd/tree/master>`_.

Initial conditions are set using second-order Lagrangian displacement (2LPT) at redshift :math:`z=9`, with a linear power spectrum based on the the transfer functions of `Eisenstein & Hu <https://background.uchicago.edu/~whu/transfer/transferpage.html>`_. The linear matter power spectrum for the fiducial cosmology can be found `here <https://github.com/jcallesh/PNG-pmwd-Suite/blob/main/docs/source/linear_powerspectrum/pmwd_matterpow_0p503.dat>`__.

Each simulation evolves :math:`512^3` dark matter particles in a periodic box of size :math:`(1 Gpc/h)^3` over 20 time steps, reaching the final redshift of :math:`z=0.5030475235459835`.

To implement primordial non-Gaussian initial conditions, we developed a modified version of the code based on the prescription by `Scoccimarro, Hui, Manera, and Chan <https://arxiv.org/abs/1108.5512>`_.

    > The updated codebase with local and equilateral templates can be found at: `pmwd PNG version <https://github.com/jcallesh/pmwd/tree/master>`_.

Each simulation is initialized with a unique random seed, consistently applied across all datasets. Specifically, simulation :math:`i` uses a seed given by :math:`10 \times i + 5`. For example, both 'LH_LC/pmwd_halos_run10.npz' and 'LH_EQ/pmwd_halos_run10.npz' are initialized with a seed value of 105.

The fiducial cosmology and simulation specifications are chosen to closely match the characteristics of the `Quijote simulations <https://arxiv.org/abs/1909.05273>`_, assuming a flat :math:`\Lambda` CDM cosmology with:

    :math:`\Omega_m=0.3175`, :math:`\Omega_b=0.049`, :math:`h=0.6711`, :math:`n_s=0.9624`, :math:`\sigma_8=0.834`, :math:`f_{NL}^{local}=0`, and :math:`f_{NL}^{equil}=0`.  

Halos are identified using a Friends-of-Friends (FoF) algorithm `(Davis, Efstathiou, Frenk, and White) <https://ui.adsabs.harvard.edu/abs/1985ApJ...292..371D>`_ with a linking length of 0.2.
We use the public `nbodykit <https://nbodykit.readthedocs.io/en/latest/index.html>`_ library and store halos containing at least 20 particles.
Dark matter particle snapshots are not stored.


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

.. toctree::
   :maxdepth: 2
   :caption: PNG-pmwd Suite

   access
   latin_hypercubes
   post-processing-data

.. toctree::
   :maxdepth: 2
   :caption: Tutorials

   Tutorial/Data_reading
   Tutorial/Powerspectrum
   Tutorial/Bispectrum

.. toctree::
   :maxdepth: 2
   :caption: Other

   team
   citation
   help
   license