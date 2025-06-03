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

To resolve this issue, you can create a folder where your user has write acess and set the environment variable 
``NUMBA_CACHE_DIR`` to it. Then add the ``NUMBA_CACHE_DIR`` environment variable to the ``envWhiteList`` in the 
`nextflow_slurm.config <https://github.com/AllenNeuralDynamics/aind-ephys-pipeline/blob/main/pipeline/nextflow_slurm.config#L117>`_.


Hugging Face cache issue: ``OSError: Read-only file system``
------------------------------------------------------------

The curation step may also fail because the Hugging Face cache is located in a read-only file system, 
such as a Singularity/Apptainer container.

Similarly to the NUMBA cache issue, you can set the environment variable ``HF_HUB_CACHE`` to a folder where your user has write access. 
Then add the ``HF_HUB_CACHE`` environment variable to the ``envWhiteList``
in the `nextflow_slurm.config <https://github.com/AllenNeuralDynamics/aind-ephys-pipeline/blob/main/pipeline/nextflow_slurm.config#L117>`_.