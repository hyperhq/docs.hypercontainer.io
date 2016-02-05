> *Note*: OS X 10.11.x is not supported yet, we are working on new Hyper Mac to support the OS X Hypervisor Framework. The Mac package is not included in the 0.5.0 release of Hyper.

## Requirements

- Hypervisor
  - [Mac OS X] VirtualBox 5.0

## Install

To install Hyper on Mac OS X, you need first to install VirtualBox 5.0, then download and Install the [hyper-mac.pkg](http://hyper-install.s3.amazonaws.com/hyper-mac.pkg)

![Hyper for Mac](https://trello-attachments.s3.amazonaws.com/55b62cf71a91815134fb04d1/620x438/1777c86bec3f4ca95ff9ff5eb8552c39/Install_Hyper_2015-07-30_00-50-54.png)

The Hyper Mac package contains

- `hyperd` Daemon, which could be controled with `launchctl`
- `hyper` cli tool with
- An uninstall shell script, located under `/opt/hyper/bin/uninstall-hyper.sh`

> If you need to uninstall hyper and clean all existing images and containers, call the uninstall script with `--purge` flag.

> VirtualBox is an open source hypervisor provided by Oracle.
