# HyperContainer Q&A

## Isolation and Resource Provision

#### Where will be applied my resource constraints which I given in the POD definition? On container level, VM level or both?

A pod of hypercontainer is run in a VM, and the resource constraints are applied to a pod (vm).

> Source: ([hyperhq/hyperd#538][hyperhq/hyperd#538])

#### Can I scale in/out any kind of resources (e.g. adding more RAM or CPU)?

The memory and cpu are hotplug-able, however, we don't scale these resources now.

> Source: ([hyperhq/hyperd#538][hyperhq/hyperd#538])

[hyperhq/hyperd#538]:https://github.com/hyperhq/hyperd/issues/538
