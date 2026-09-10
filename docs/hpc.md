# High-Performance Computing Cluster

## Summary

The [high-performance compute](https://en.wikipedia.org/wiki/High-performance_computing) (HPC) cluster is the "brain" of the ACC-UB infrastructure, featuring powerful hardware for solving the most advanced scientific problems, including: numerical simulations, big data processing, machine learning etc.

The servers run [Linux](https://en.wikipedia.org/wiki/Linux), more specifically [Ubuntu Server](https://ubuntu.com/download/server) 24.04. They feature a shared filesystem ([NFS v4.2](https://en.wikipedia.org/wiki/Network_File_System) and [NVMe over TCP](https://en.wikipedia.org/wiki/NVMe_over_TCP)), [InfiniBand](https://en.wikipedia.org/wiki/InfiniBand) for high-speed inter-node communication and [RDMA](https://en.wikipedia.org/wiki/Remote_direct_memory_access), as well as an [environment modules](https://envmodules.io/) system. Job scheduling is handled by [SLURM](slurm.md).


## CPU nodes

### Hardware configuration

The compute system currently consists of 22 identical nodes, with the following hardware specifications:

- **CPU:** AMD EPYC 7713 (2 sockets, each with 64 cores, for 128 physical cores; due to hyperthreading, we have 256 hardware threads)

- **Memory:** 2 TiB of RAM

- **Storage**: the root filesystem is installed on 3 NVMe drives in RAID 5 configuration (so we only have 3.5 TiB available space in total). Each node is also connected to the shared network storage (available under `/mnt`), which has a capacity of 32+ TiB.

The nodes `ctrl01` and `db01` are used for additional tasks (SLURM controller, SLURM accounting database, NFS v4.2 server etc), so parts of their cores and memory are reserved for system tasks.

## GPU node

### Hardware configuration

The GPU node we have is equipped with the following:

- **CPU**: Intel Xeon Platinum 8480+ (2 sockets, each with 56 cores; due to hyperthreading, we have 224 hardware threads)
- **Memory**: 2 TiB of RAM
- **Storage**: the root filesystem is installed on 2 NVMe drives in RAID 1 configuration (so we only have 1.7 TiB available space in total). There are 8 more NVMe drives used by various faculties and research groups, each with a capacity of 3.5 TiB. The node is also connected to the shared network storage (available under `/mnt`), which has a capacity of 32+ TiB.
- **GPUs**: 8 × NVIDIA H100, 80 GiB of VRAM each

Since the cores and memory are shared with all other users on the node, please be mindful of your usage.

### Using the GPUs on the HPC-GPU node

To access the GPUs, your job must be submitted to the `gpu` partition and must explicitly request them by using the `--gpus` flag in SLURM.

Be aware that some of the GPUs are currently dedicated/reserved for certain research groups, so not all of them might be available to SLURM.
