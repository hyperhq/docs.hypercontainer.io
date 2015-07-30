# What is Pod

Pod is a concept originated from [Google](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md). According to [Google Kuberenetes](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md):

    In Kubernetes, rather than individual application containers, Pods are the smallest deployable units that can be created, scheduled, and managed.

    A Pod (as in a pod of whales or pea pod) corresponds to a colocated group of applications running with a shared context. Within that context, the applications may also have individual cgroup isolations applied. A Pod models an application-specific "logical host" in a containerized environment. It may contain one or more applications which are relatively tightly coupled -- in a pre-container world, they would have executed on the same physical or virtual host.

The key idea behind **Pod** is that in a microservice architecture usually involves some "helper" programs, such as log, monitoring, cron, etc. These helper programs are built to work cooperatively with the app. Therefore, instead of running in multiple isolated containers, these processes should share the namespace, though they are packaged in different images.

## Pod is the first class in Hyper

In Hyper, a pod consists of a colocated group of AppContainer images, deployed as a single unit in one Hyper instance.

	[root@user ~:]# hyper run -p nginx rails logstash cronjob

Inside of the instance, multiple applications from different images share the namespaces: ***`PID`***, ***`Network`***, ***`IPC`***, ***`UTS`***, ***`User`***. Pod helps to provide a familiar view of a tranditional OS to applications, rather than the philosophy of "*one process per container*":

- Processes can see each other
- Processes can use all IPC facilities to communicate
- Processes share the same hostname
- Processes have access to all NICs attached to the instance, and share the same port range
- Processes have access to all disk attached to the instance

The exception is ***`Mount`***. Since a Pod may have multiple app images, Hyper applies the ***`Mount`*** namespace to isolate the root filesystem from each other.

Note: Hyper is immune from [Pid  1 problem](https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/), since HyperStart launches the app processes and continues to live in the same namespace with them.
