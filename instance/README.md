# HyperVM

HyperVM is the VM instances booted the minimalist HyperKernel. A HyperVM is loaded with a single [pod](../pod/README.md), which runs a group of containers.

, a Pod could run on top of a vm, and stop on it, and VM does not has persistent status, will be reclaim after shutdown.

A running VM has 2 state:

- **Associated** with a Pod, or
- **Idle**
