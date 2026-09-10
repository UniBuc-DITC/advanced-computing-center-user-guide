# SLURM User Guide

## Summary

The HPC cluster uses [Slurm workload manager](https://slurm.schedmd.com/overview.html) as our job scheduler. This page provides an overview of our Slurm config, basic usage and best practices.

Reading the official [Slurm user guide](https://slurm.schedmd.com/quickstart.html) as well is recommended.

## Running jobs on the CPU cluster

To launch a job, connect to the **controller node** and either use the `srun` command (for interactive jobs) or the `sbatch` command (for batch jobs / scripts).

If your program/tool is using the [Message-Passing Interface](https://en.wikipedia.org/wiki/Message_Passing_Interface) for parallelization, you can run the `mpirun` command under Slurm to automatically distribute the work across all of the nodes requested by your job.

Most programs with support for parallelization will also provide instructions for how to run the software on a cluster with Slurm.

### Slurm web interface

While your job runs, you can check its status and resource utilisation by running the `squeue` command. To allow for friendlier and more interactive monitoring of a job's status, we have also installed and configured the [Slurm web](https://slurm-web.com/) dashboard.

To access the web UI, navigate to <https://hpc-ctrl01.acc-ub.local> (your browser will likely warn you about untrusted certificates; accept them or skip the warning), then log in with your ACC user credentials. You'll be able to check the system's status, load, job queue and job details.

### Using `mpi4py` (MPI for Python)

If you use [the Python bindings for MPI](https://mpi4py.readthedocs.io/en/stable/), you should use them together with an MPI implementation available as a module on the HPC system (i.e. OpenMPI or MPICH). To use this installation, activate the corresponding modules: `module add mpi/openmpi` or `module add mpi/mpich`.

If you use `conda` to manage your packages, you might find it automatically installs a generic MPI implementation, which will lead to errors, such as:

```
A requested component was not found, or was unable to be opened.  This
means that this component is either not installed or is unable to be
used on your system (e.g., sometimes this means that shared libraries
that the component requires are unable to be found/loaded).  Note that
PMIx stopped checking at the first component that it did not find.

Host:      hpc-ctrl01.acc-ub.local
Framework: psec
Component: munge
```

You should follow [these instructions from `conda-forge`](https://conda-forge.org/docs/user/tipsandtricks/#using-external-message-passing-interface-mpi-libraries) on how to use an external MPI library. You will have to run a command such as `conda install "openmpi=X.Y.*=external_*"` or `conda install "mpich=X.Y.*=external_*`, where `X.Y` should match the major and minor version numbers for your selected MPI implementation module. This will also require you to have the corresponding module active whenever you run a Python program which uses `mpi4py`.

## Running jobs on the GPU node

The available GPU resources are managed through Slurm's [GRES](https://slurm.schedmd.com/gres.html) system.

To run a job which requires one or more GPU devices, pass the `--partition=gpu --gpus=<number of GPUs>` flags to SLURM.

For more specific resource allocation (for example, if you want a specific GPU), use the `--gres` flag: `--gres=gpu:nvidia_h100_80gb_hbm3:<num_gpus>`
