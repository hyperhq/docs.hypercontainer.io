# Why Hyper

Hyper combines the best from both worlds: ***Virtualization*** and ***Docker***.


## Security

Virtualization offers an excellent security. The attack surface for a VM instance is quite small, as it lacks the variety of functions (and, therefore, the potential flaws to be exploited) provided by standard operating systems.

More important, Hyper is immune from the isolation problem in container.

## Immutable

Hyper eliminates the need for guest OS. There are no moving parts inside of a Hyper instance to be configured or managed, only the kernel and the loaded Docker images.

Therefore the entire stack is immutable.

## Compatibility

Since each VM instance runs its own kernel, tenants have the choice to pick their favorite kernel version and modules, based on the application requirements.

## Mature

Compared with container, virtualization is production-ready. Features like LiveMigration, SDN, SDS are battle-tested for years. Hyper lets you enjoy all these features without any integration work.

## Seamless Migration

Virtualization are widespread among enterprises. Many of them have a virtualized infrastructure running. Instead of having to rebuild everything with container, Hyper provides a seamless migration path to adopt Docker.

## Hypervisor Agnostic

Hyper is designed to be independent from the underlying virtualization technology. [The current implementation](----TODO----) supports KVM and Xen, with more virtualization technologies in the roadmap.


You can find the more detailed comparision between Hyper and other solutions in the follow articles:

- Container-centric OS (CoreOS, RancherOS, etc)
-
