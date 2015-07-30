# Version 0.3 (2015-07-30)

The 0.3 release brings Hyper to **Mac OS X**. See the detail updates of Hyper 0.3.

## Highlight features

- Hyper Mac with Pods and Volumes support.
- New Hypervisor support: VirtualBox 5.0, the widely adopted open source hypervisor runs on Mac OS X and other platforms.
- New Graph Driver: VDI, layered storage based on VirtualBox differencing VDI image, working like the devicemapper driver. Because the VDI layered images are maintained by a Hyper VM, it is platform indenpendent and works well on Darwin.
- Image management functions (only for Mac OS X in this version), including `pull`, `push`, `images`, `rmi`, `commit`.
- Support build standard Docker image with `Dockerfile.`
- Optimized guest kernel, and could start a Pod in less than 2.5 seconds.

## Other improvements

These features are shipped with Mac version, but will be available on the Linux version soon.

- Support `--rm` flag for `run` command, now it can automatically remove a Pod, when finished.
- Support remove multiple Pod in one `rm` command line.
- Many bug fix.

More details on the web site [(http://hyper.sh)](http://hyper.sh/).

> VirtualBox is an open source hypervisor by Oracle.
