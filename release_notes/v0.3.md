# Version 0.3 (2015-07-30)


The 0.3 release brings Hyper to **Mac OS X**. See the detail updates of Hyper 0.3.

## Highlight features

- Hyper Mac with Pod and Volume support.
- New Hypervisor support: VirtualBox 5.0, the widely adopted open source hypervisor runs on Mac and other platforms. 
- New Graph Driver: VDI, layered storage based on virtualbox differencing vdi image, working like the devicemapper driver. And because the VDI layered images are maintained() by a Hyper VM, it is platform indenpendent and works well on Darwin.
- Image management functions (only on Mac in this version), including `pull`, `push`, `images`, `rmi`, `commit`.
- Support build standard docker image with `Dockerfile.`
- Optimized guest kernel, and could start a Pod in less than 2.5 seconds.

## Other improvements

These features are shipped with Mac version and will return to the linux version soon.

- Support `--rm` flag for `run` command, now it can automaticclly remove pod after pod finish.
- Support remove multiple pod in one `rm` command line.
- Many bug fix.

More details on the web site [(http://hyper.sh)](http://hyper.sh/).

> VirtualBox is an open source hypervisor by Oracle.
