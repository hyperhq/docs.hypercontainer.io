# Install

### Requirements

- QEMU 2.0 or later
- Docker 1.5 or later

### Setup

To set Hyper up, simply

    curl -sSL https://hyper.sh/install | bash

Please note that [the current version](../release_notes/latest.md) supports the following Linux distro:

- Ubuntu 64bit
	- 15.04 Vivid
	- 14.10 Utopic
	- 14.04 Trusty
- CentOS 64bit
	- 7.0
	- 6.x (upgrade to QEMU 2.0)
- Fedora 20-22 64bit
- Debian 7.4 wheezy 64bit (upgrade to QEMU 2.0)

### Build from source

#### Daemon and CLI client:

Clone hyper in GoPath

    > cd ${GOPATH}/src
	> git clone https://github.com/hyperhq/hyper.git hyper

And make sure you have `go` (>= 1.4), `godep`, and `autotools`, go into the `hyper` dir

    > ./autogen.sh
    > ./configure
    > make

(If you do not want to build with xen support, use configure option `--without-xen`.)

Then you can get the binaries `hyperd` daemon and `hyper` cmdline tool. 

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

Then you can find `hyper-initrd.img` in build directory, together with a pre-build `kernel`. You can also found the `kernel_config` in the repo.

