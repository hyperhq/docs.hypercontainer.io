## Build from source

#### Daemon and CLI client:

Clone hyper in GoPath

    > cd ${GOPATH}/src
    > mkdir -p github.com/hyperhq
    > cd github.com/hyperhq
    > git clone https://github.com/hyperhq/hyperd.git hyperd
    > git clone https://github.com/hyperhq/runv.git runv

And make sure you have `go` (>= 1.5, 1.7 or later is recommended) and `autotools`, develop files of
`libdevmapper`, `libsqlite3`, `libvirt-devel` then

    > cd hyper
    > ./autogen.sh
    > ./configure
    > make

(If you want to build without Xen support, use configure option `--without-xen`.)

Then you can get the binaries `hyperd` daemon and `hyperctl` CLI tool.

#### Build Xen from source

Download Xen 4.5.0 or later version, and configure with the following option

    > ./configure --with-extra-qemuu-configure-args="--enable-virtfs"

#### Guest Kernel and Initrd

Clone hyperstart

    > git clone https://github.com/hyperhq/hyperstart.git hyperstart

And build with autotools

    > ./autogen.sh
    > ./configure
    > make

Then you can find `hyper-initrd.img` in build directory, together with a pre-build `kernel`. You can also find the `kernel_config` in the repo.

#### Build Qemu

Hyperd could work with vanilla qemu 2.0 or newer, however, we provided our branch with some patches from hyper:

```
https://github.com/hyperhq/qemu/tree/2.4.1-template
```

If you build Qemu from source, don't forget enable virtfs (`--enable-virtfs`) during configuration.

#### Build Your Own Kernel

You can reference the [Hyper kernel configuration](https://github.com/hyperhq/hyperstart/blob/master/build/kernel_config).

You can find related configuration items in [the config file](../../reference/configuration.html).
