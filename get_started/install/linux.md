## Requirements

- Hypervisor: at least one of
  - [Linux] QEMU 2.0 or later
  - [Linux] Xen 4.5 or later (for Xen support)

## Install

[the current version](../release_notes/latest.md) supports the following Linux distros:

- Ubuntu ( > 14.04 )
- CentOS/RHEL 7.x
- Fedora ( > 20 )
- Debian ( > 7.0 )

### curl-to-bash or tarball

To setup Hyper, simply run (after 0.4, the same package support both
  KVM and Xen)

    curl -sSL https://hyper.sh/install | bash

Don't like the "curl to bash" methods? Download [tarball here](http://hyper-install.s3.amazonaws.com/hyper-latest.tgz).

For CentOS/RHEL users, please use the pre-build RPMs

If you build Qemu from source, don't forget enable virtfs (`--enable-virtfs`) during configuration.

### RPMs for CentOS/RHEL7

x86_64 binary packages:

> - [hyper-0.4-2.el7.centos.x86_64.rpm](https://s3.amazonaws.com/hyper-install/hyper-0.4-2.el7.centos.x86_64.rpm)
> -  [hyperstart-0.4-2.el7.centos.x86_64.rpm](https://s3.amazonaws.com/hyper-install/hyperstart-0.4-2.el7.centos.x86_64.rpm)
> - [qemu-hyper-2.4.1-2.el7.centos.x86_64.rpm](https://s3.amazonaws.com/hyper-install/qemu-hyper-2.4.1-2.el7.centos.x86_64.rpm)

soruce RPMs:

> - [hyper-0.4-2.el7.centos.src.rpm](https://s3.amazonaws.com/hyper-install/hyper-0.4-2.el7.centos.src.rpm)
> - [hyperstart-0.4-2.el7.centos.src.rpm](https://s3.amazonaws.com/hyper-install/hyperstart-0.4-2.el7.centos.src.rpm)
> - [qemu-hyper-2.4.1-2.el7.centos.src.rpm](https://s3.amazonaws.com/hyper-install/qemu-hyper-2.4.1-2.el7.centos.src.rpm)
