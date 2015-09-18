# How it works

Hyper has four components:

  - CLI: ***hyper***
  - Daemon: ***hyperd*** (with REST APIs)
  - Guest Kernel: ***hyperkernel***
  - Guest Init Service: ***hyperstart***

On a physical Linux host:

        [root@user ~:]# hyper pull nginx:latest
        [root@user ~:]# hyper run nginx:latest

Upon ***RUN***, Hyper launches the Docker images with a new VM instance, instead of Linux containers:

        [root@user ~:]# docker ps
        [root@user ~:]#
        [root@user ~:]# hyper list
        ......
        Done

Internal to the HyperVM, a minimalist Linux kernel, called ***HyperKernel***, is booted. The kernel employs a tiny Init service, called ***HyperStart*** to load the Docker images from the host, setup *MNT* namespace to isolate their filesystems, and launch them.

![](https://trello-attachments.s3.amazonaws.com/554c998a4c9dacc5c143ec99/1083x635/c8748abc93dbc18e70f7a09d2963e8ff/hyper.png)
