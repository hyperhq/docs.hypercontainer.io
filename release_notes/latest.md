# Version 0.5 (2016-02-05)

In version 0.5, Hyper and runV introduced many features, improved stability, and fixed many bugs.

## Highlight features

- Optimized the `run` command, for example, now you can use `-t` flag for tty. more flags definition could reference the [run command](../reference/run.md).
- Support `libvirt` as an hypervisor driver, and with libvirt, you can find Hyper VMs with `virsh`
- Support service-discovery aux container in Pod and other related features for the integration with Kubernetes.
- Support Cinder/ceph volume and configured Neutron Networks for the integration with OpenStack.
- Allow configure storage driver through config file.

## Other improvements

- Allow attach to containers from the very beginning.
- Improve file insert, now you can insert files from either remote or local machine by specify the URI.
- Hyper client now return the exit value of the process when `run` or `exec` exit.
- Configure default `/etc/hosts` and `/etc/resolv.conf` for the user if no hosts or DNS configured.
- Improve `list` command, now you can list contents with vm or pod as filter.
- Support `logs` command for container logs.
- Support registry mirror and insecure registry options.
- Build RPM packages for CentOS and Fedora with Hyper.
- Add integration tests.
- Many stability improvements and bug fixes.

More details on our website: [(http://hypercontainer.io)](http://hypercontainer.io/).
