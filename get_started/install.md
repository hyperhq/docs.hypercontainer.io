# Install

## Requirements

- Docker 1.5 or later
- Hypervisor
  - [Linux] QEMU 2.0 or later
  - [Linux] Xen 4.5 or later (for Xen support)
  - [Mac OS X] VirtualBox 5.0

## Install on Linux

To set Hyper up, simply (kvm version)

    curl -sSL https://hyper.sh/install | bash

or (xen version, include kvm support too, but has dependency of xen 4.5 library)

    curl -sSL https://hyper.sh/install-xen | bash

Don't like the "curl to bash" methods? Download tarball here: [kvm version](http://hyper-install.s3.amazonaws.com/hyper-latest.tgz), [xen version](http://hyper-install.s3.amazonaws.com/hyper-xen-latest.tgz).

Please note that [the current version](../release_notes/latest.md) supports the following Linux distro:

- Ubuntu 64bit
	- 15.04 Vivid
	- 14.10 Utopic
	- 14.04 Trusty
- CentOS 64bit
	- 7.0
	- 6.x (upgrade to QEMU 2.0)
- Fedora 20-22 64bit
- Debian 64bit
    - 8.0 jessie
    - 7.x wheezy (upgrade to QEMU 2.0)

## Install on Mac

To install Hyper for Mac, you need install VirtualBox 5.0, then download and Install the [hyper-mac.pkg](http://hyper-install.s3.amazonaws.com/hyper-mac.pkg)

![Hyper for Mac](https://trello-attachments.s3.amazonaws.com/55b62cf71a91815134fb04d1/620x438/1777c86bec3f4ca95ff9ff5eb8552c39/Install_Hyper_2015-07-30_00-50-54.png)

The Hyper Mac contains 

- `hyperd` Daemon, which could be controled with `launchctl`
- `hyper` cli tool with
- An uninstall shell script at `/opt/hyper/bin/uninstall-hyper.sh`

> If you need uninstall hyper and clean all existing images and containers, call the uninstall script with `--purge` flag. 

> VirtualBox is an open source hypervisor by Oracle.

## Build from source

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

#### Build Your Own Kernel

You can reference the [hyper kernel configuration](https://github.com/hyperhq/hyperstart/blob/master/build/kernel_config),
and for Qemu/Kvm driver, you'd better build new CBFS rom with `make cbfs`, which will add kernel in `build/` and initramfs
into a CBFS ROM. 

You can find related configuration items in [the config file](../reference/configuration.html).

