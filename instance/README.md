# HyperVM

HyperVM is the VM instance booted by the minimalist HyperKernel. A HyperVM is loaded with a single [Pod](../pod/README.md), which runs a group of containers.

A Pod could run on top of a VM, or stop on it. A VM does not have persistent status: they will be reclaimed after shutdown.

A running VM has 2 state:

- **Associated** with a Pod, or
- **Idle**
