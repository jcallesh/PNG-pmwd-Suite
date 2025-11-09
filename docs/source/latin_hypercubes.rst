.. _latin_hypercubes:

****************
Latin-hypercubes
****************


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

The Latin hypercubes values can also be found in `here <https://github.com/jcallesh/PNG-pmwd-Suite/tree/main/docs/source/Latin_hypercube>`__.


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

Check the Tutorial notebook `(here) <https://github.com/jcallesh/PNG-pmwd-Suite/blob/main/docs/source/Tutorial/Data_reading.ipynb>`_.