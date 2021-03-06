# BUDE Benchmark

This repository contains implementation of the core computation of the Bristol University Docking Engine (BUDE) in different HPC programming models.
The benchmark is a virtual screening run of the NDM-1 protein and runs the energy evaluation for a single generation of poses repeatedly, for a configurable number of iterations.
Increasing the iteration count has similar performance effects to docking multiple ligands back-to-back in a production BUDE docking run.

## Structure

The top-level `data` directory contains the input common to implementations.
The top-level `makedeck` directory contains an input deck generation program and a set of mol2/bhff input files.
Each other subdirectory contains a separate implementation:

- [OpenMP](openmp/) for CPUs
- [SYCL](sycl/) for CPUs
- [OpenMP target](openmp-target/) for GPUs
- [OpenCL](opencl/) for GPUs
- [CUDA](cuda/) for GPUs
- [OpenACC](openacc/) for GPUs

## Building

To build with the default options, type `make` in an implementation directory.
There are options to choose the compiler used and the architecture targetted.

Refer to each implementation's README for further build instructions.

## Running

To run with the default options, run the binary without any flags.
To adjust the run time, use `-i` to set the number of iterations.
For very short runs, e.g. for simulation, use `-n 1024` to reduce the number of poses.
The maximum number of poses supported is `65536`.

Refer to each implementation's README for further run instructions.

### Benchmarks

Two input decks are included in this repository:

* `bm1` is a short benchmark (~100 ms/iteration on a 64-core ThunderX2 node) based on a small ligand (26 atoms)
* `bm2` is a long benchmark (~25 s/iteration on a 64-core ThunderX2 node) based on a big ligand (2672 atoms)

They are located in the [`data`](data/) directory, and `bm1` is run by default.
All implementations accept a `--deck` parameter to specify an input deck directory.
See [`makedeck`](makedeck/) for how to generate additional input decks.
