# FAQ on Xen Support

## Xen Installation

#### What are the Xen installation requirements?

- Xen 4.5 or later
- HVM support. (check it with `xl info`)

#### I have Xen 4.4, does it work?

No. Xen 4.4 do not support hvm direct boot, we are working on other methods, but they were not included in the current release. Pull requests are always welcome.

#### I have Xen 4.5 installed, but can not load Xen driver in Hyper.

Please make sure the `xenstored` running. You could start it with

    /etc/init.d/xencommons start

#### I have Xen 4.5 installed, but can not start a domain with Hyper.

You need *VirtFS* support to run hyper, try configure Xen with the following flag:

    ./configure --with-extra-qemuu-configure-args="--enable-virtfs"

#### I have VirtFS support, but I can not start a domain either.

If you found this message log:

    Could not allocate memory for HVM guest. (16 = Device or resource busy): Internal error

You should limit the Xen dom0 memory, try this Xen command line option in `grub.cfg`: `dom0_mem=1024M`

## Build from Source

#### I met many cgo errors when I build from sources.

Old versions of go compiler has issues with the cgo code. Try to update go to version 1.4 or later

#### I met some "undefined reference" error.

If you met errors like `undefined reference to 'libxl_mac_copy'`, you may have development files of older Xen versions, try to uninstall them. (such as package `libxen-dev`)
