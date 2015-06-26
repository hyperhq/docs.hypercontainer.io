# FAQ on Xen Support

## Xen Installation

#### What are the Xen installation requirements?

- Xen 4.5 or later
- hvm support. (check it with `xl info`)

#### I have xen 4.4, does it work?

No. Xen 4.4 do not support hvm direct boot, we are working on other methods, but they were not included in the current release. Pull requests are always welcome.

#### I have xen 4.5 installed, but can not load Xen driver in hyper.

Please make sure the `xenstored` running. You could start it with 

    /etc/init.d/xencommons start

#### I have xen 4.5 installed, but can not start a domain with hyper.

You need *VirtFS* support to run hyper, try configure xen with the following flag:

    ./configure --with-extra-qemuu-configure-args="--enable-virtfs"

#### I have virtfs support, but I can not start a domain either.

If you found this message log:

    Could not allocate memory for HVM guest. (16 = Device or resource busy): Internal error

You should limit the xen dom0 memory, try this xen command line option in `grub.cfg`: `dom0_mem=1024M`

## Build from Source

#### I met many cgo errors when I build from source.

Old version of go compiler has issues with the cgo code. Try update to go 1.4 or later

#### I met some "undefined reference" error.

If you met errors like `undefined reference to 'libxl_mac_copy'`, you may have development files of older xen version, try uninstall them. (such as package `libxen-dev`)
