# FAQ on Qemu/Kvm Support

## Start a Hyper Pod

#### Fail to start hyper VM while there is a VirtualBox VM running.

If the virtualbox (Oracle VM) is started with kernel extension, it will occuppy the kvm device. If you want to run hyper, you should stop virtualbox, or disable the kernel extension of it, which will make the virtualbox vm run much slower.

## Build from Source

#### I build my own qemu 2.x, but can not run hyper pod

The default qemu configurate does not include virtfs support, config it with `--enable-virtfs` to enable it.
