.. _troubleshooting:

Troubleshooting
===============

This section provides solutions to common issues encountered while using the AIND Ephys Pipeline. 
If you encounter a problem not listed here, please consider opening an issue on our GitHub repository.


NUMBA cache issue: ``RuntimeError: cannot cache function``
----------------------------------------------------------

The curation step may fail because NUMBA cannot cache the compiled functions to the location where the 
Python environment is installed. This can happen if the environment is installed in a read-only location, such as a 
Singularity/Apptainer container.

To resolve this issue, you can create a folder where your user has write access and set the environment variable 
``NUMBA_CACHE_DIR`` to it. 

Hugging Face cache issue: ``OSError: Read-only file system``
------------------------------------------------------------

The curation step may also fail because the Hugging Face cache is located in a read-only file system, 
such as a Singularity/Apptainer container.

Similarly to the NUMBA cache issue, you can set the environment variable ``HF_HUB_CACHE`` to a folder where your user has write access. 


Matplotlib cache issue: ``OSError: Read-only file system``
----------------------------------------------------------

The cache issue can also occur with Matplotlib, which may try to write to a read-only file system
in the visualization step.

Again, you can set the environment variable ``MPLCONFIGDIR`` to a folder where your user has write access. 


.. note::

    To make these changes persistent, you can add the following lines to your ``.bashrc`` or ``.bash_profile`` file:
    .. code-block:: bash

        export NUMBA_CACHE_DIR=/path/to/your/cache/dir
        export HF_HUB_CACHE=/path/to/your/cache/dir
        export MPLCONFIGDIR=/path/to/your/cache/dir

    The three environment variables are already in the singularity ``envWhiteList`` of the `nextflow_slurm.config <>`_ 
    file, so they will be automatically used automatically if defined.