# How it works

Hyper has four components:

  - CLI: ***hyper***
  - Daemon: ***hyperd*** (with REST APIs)
  - Guest Kernel: ***hyperkernel***
  - Guest Init Service: ***hyperstart***

On a physical Linux host:

        [root@user ~:]# docker pull nginx:latest
        [root@user ~:]# hyper run nginx:latest

Upon the ***RUN*** command, Hyper launches a new VM instance, instead of containers, and mount the specified image onto the instance:

        [root@user ~:]# docker ps
        [root@user ~:]#
        [root@user ~:]# hyper list
        ......
        Done

Internal to the VM, a minimalist Linux kernel, called ***HyperKernel***, is booted. HyperKernel is built with a tiny Init service, called ***HyperStart***, which create a ***Pod***, setup *Mount* namespace, and launch apps from the loaded images.

![](https://trello-attachments.s3.amazonaws.com/554c998a4c9dacc5c143ec99/1083x635/08dfe9e383fb0b566986fc76e3a2c8c1/hyper_2.png)




