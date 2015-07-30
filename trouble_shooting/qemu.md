# FAQ on Qemu/KVM Support

## Start a Hyper Pod

#### Fail to start Hyper VM while there is a VirtualBox VM running.

If the VirtualBox (Oracle VM) is started with a kernel extension, it will occupy the KVM device. If you want to run Hyper, you should stop VirtualBox, or disable its kernel extension, which will make the VirtualBox VM run much slower.

## Build from Source

#### I built my own Qemu 2.x, but cannot run Hyper Pod

The default Qemu configuration does not include virtfs support, configure it with `--enable-virtfs` to enable it.
