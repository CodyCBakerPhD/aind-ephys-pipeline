.. _troubleshooting:

Troubleshooting
===============

This section provides solutions to common issues encountered while using the AIND Ephys Pipeline. 
If you encounter a problem not listed here, please consider opening an issue on our GitHub repository.


``RuntimeError: cannot cache function`` NUMBA failure in curation
-----------------------------------------------------------------

The curation step may fail because NUMBA cannot cache the compiled functions to the location where the 
Python environment is installed. This can happen if the environment is installed in a read-only location, such as a 
Singularity/Apptainer container.

To resolve this issue, you can create a folder where your user has write acess and set the environment variable 
``NUMBA_CACHE_DIR`` in the `nextflow_slurm.config <https://github.com/AllenNeuralDynamics/aind-ephys-pipeline/blob/main/pipeline/nextflow_slurm.config#L117>`_ to it.
