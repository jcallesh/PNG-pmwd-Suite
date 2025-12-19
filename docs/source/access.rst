.. _data_access:

***********
Data Access
***********

The PNG-pmwd data is publicly available through the `Globus <https://www.globus.org/>`__ file transfer service.

You can access the collection directly using the following link:

`PNG-pmwd Globus Collection <https://app.globus.org/file-manager?origin_id=c1ae3f00-2c11-474a-b8d9-fe263a3ecdbb&origin_path=%2F&two_pane=false>`__

or search:

- **Collection Name:** wisc-drive-gshiu  
- **Collection ID:** ``c1ae3f00-2c11-474a-b8d9-fe263a3ecdbb``  
- **Data Path:** ``/PNG-pmwd/``

Data can be downloaded directly via the Globus web interface.  
For instructions, see: https://docs.globus.org/guides/tutorials/manage-files/transfer-files/


Data Organization
-----------------

The PNG-pmwd data are organized within the directory::

    /PNG-pmwd/

The relevant subdirectories and files are structured as follows:

.. code-block:: text

    /PNG-pmwd/
    ├── Halo_catalogs/
    │   ├── LH_{Dataset}/
    │   │   ├── pmwd_halos_run0.npz      # Halo catalog data
    │   │   ├── pmwd_halos_run0.json     # Metadata for the corresponding halo catalog
    │   │   │
    │   │
    │   ├── latin_hypercube_params_{Dataset}.txt   # Latin hypercube parameter values
    │   │
    ├── PSBS.tar                         # All power spectrum measurements (tar archive)

Here, ``{Dataset}`` corresponds to the labels described in the
`Latin Hypercube table <latin_hypercubes.html>`_.


Command Line Interface
----------------------

You may also download the data using the Globus Command Line Interface (CLI).  

- Installation instructions: https://docs.globus.org/cli/  
- Quickstart guide: https://docs.globus.org/cli/quickstart/
- More examples: https://docs.globus.org/cli/reference/transfer/

For example, to download the ``LH_LC300`` dataset to your local machine, follow these steps:

.. code-block:: bash

    # Define source and destination endpoints
    source_ep=c1ae3f00-2c11-474a-b8d9-fe263a3ecdbb
    dest_ep=<your-endpoint-ID>

    # Run the transfer command
    globus transfer \
        $source_ep:/PNG-pmwd/Halo_catalogs/LH_LC300/ \
        $dest_ep:~/local_path/ \
        --label "CLI PNG-pmwd LH_LC300" \
        --recursive

To find your endpoint ID, run:

.. code-block:: bash

    globus whoami -v

Look for a line containing your endpoint ID, for example: ``ID 313ce13e-b597-5858-ae13-29e46fea26e6``.
