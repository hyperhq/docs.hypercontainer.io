# What is Pod

Pods is the first-class unit for app deployment and execution in DVM.

According to [Google Kuberenetes](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md):

    In Kubernetes, rather than individual application containers, pods are the smallest deployable units that can be created, scheduled, and managed.

    A pod (as in a pod of whales or pea pod) corresponds to a colocated group of applications running with a shared context. Within that context, the applications may also have individual cgroup isolations applied. A pod models an application-specific "logical host" in a containerized environment. It may contain one or more applications which are relatively tightly coupled -- in a pre-container world, they would have executed on the same physical or virtual host.

The key idea behind **Pod** is that in a microservie architecture usually involves some "helper" programs, such like log, monitoring, cron, etc. These helper programs are built to work co-operatively with the app. Therefore, instead of running in multiple isolated containers, these processes should share the same environment, although they are packaged in different images.

In terms of DVM, a pod consists of a colocated group of Docker images, deployed as an atomic unit and loaded into the same DVM instance.

The context of the pod can be defined as the conjunction of:

- **PID**: processes within the pod can see each other)
- **Network**: processes within the pod have access to all NICs attahed with the instance, and they share the same IP and port space
- **IPC**: processes within the pod can use SystemV IPC or POSIX message queues to communicate
- **UTS**: processes within the pod share a hostname)
- **Filesystem**: processes within the pod cannot see each other's root filesystem
- **Volume**: processes within a pod have access to all volumes attached with the instance
- **Device**:
