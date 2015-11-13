## Requirements

- Hypervisor: at least one of
  - [Linux] QEMU 2.0 or later
  - [Linux] Xen 4.5 or later (for Xen support)

## Install
To setup Hyper, simply run (after 0.4, the same package support both
  KVM and Xen)

    curl -sSL https://hyper.sh/install | bash

Don't like the "curl to bash" methods? Download [tarball here](http://hyper-install.s3.amazonaws.com/hyper-latest.tgz).

Please note that [the current version](../release_notes/latest.md) supports the following Linux distros:

- Ubuntu 64bit
	- 15.04 Vivid
	- 14.10 Utopic
	- 14.04 Trusty
- CentOS 64bit (manually build QEMU 2.0 or above)
	- 7.0
	- 6.x
- Fedora 20-22 64bit
- Debian 64bit
    - 8.0 jessie
    - 7.x wheezy (upgrade to QEMU 2.0)

If you build Qemu from source, don't forget enable virtfs (`--enable-virtfs`) during configuration.
