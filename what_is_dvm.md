<<<<<<< HEAD
# Why DVM

DVM combines the best from both worlds: ***Virtualization*** and ***Docker***.


## Security

Virtualization offers an excellent security. The attack surface for a VM instance is quite small, as it lacks the variety of functions (and, therefore, the potential flaws to be exploited) provided by standard operating systems.

More important, DVM is immune from the isolation problem in container.

## Immutable

DVM eliminates the need for guest OS. There are no moving parts inside of a DVM instance to be configured or managed, only the kernel and the loaded Docker images.

Therefore the entire stack is immutable.

## Compatibility

Since each VM instance runs its own kernel, tenants have the choice to pick their favorite kernel version and modules, based on the application requirements.

## Mature

Compared with container, virtualization is production-ready. Features like LiveMigration, SDN, SDS are battle-tested for years. DVM lets you enjoy all these features without any integration work.

## Seamless Migration

Virtualization are widespread among enterprises. Many of them have a virtualized infrastructure running. Instead of having to rebuild everything with container, DVM provides a seamless migration path to adopt Docker.

## Hypervisor Agnostic

DVM is designed to be independent from the underlying virtualization technology. [The current implementation](----TODO----) supports KVM and Xen, with more virtualization technologies in the roadmap.


You can find the more detailed comparision between DVM and other solutions in the follow articles:

- Container-centric OS (CoreOS, RancherOS, etc)
-
=======
# What is DVM
>>>>>>> 26433cb1893c6bfee96baadd76bb9424da308497
