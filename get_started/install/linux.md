## Requirements

- Docker 1.5 or later
- Hypervisor
  - [Linux] QEMU 2.0 or later
  - [Linux] Xen 4.5 or later (for Xen support)

## Install
To setup Hyper, simply run (KVM version)

    curl -sSL https://hyper.sh/install | bash

or (xen version, includes KVM support too, but depends of Xen 4.5 library)

    curl -sSL https://hyper.sh/install-xen | bash

Don't like the "curl to bash" methods? Download tarballs here: [KVM version](http://hyper-install.s3.amazonaws.com/hyper-latest.tgz), [Xen version](http://hyper-install.s3.amazonaws.com/hyper-xen-latest.tgz).

Please note that [the current version](../release_notes/latest.md) supports the following Linux distros:

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
