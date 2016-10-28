# Lifecycle

![](https://trello-attachments.s3.amazonaws.com/5562ba47387906ddef327e00/704x249/e4b1ec0168197c13e838bd5b405b3f28/pod.png)

In Hyper, a Pod has two states:

- `Created`: a Pod is defined, its storage has been allocated, and the Docker images have been downloaded
- `Running`: a Pod (with its containers) is launched in a VM instance


A Pod can be launched either explicitly:

	[root@user ~:]# hyperctl run -p podfile.json

Or, implicitly:

	[root@user ~:]# hyperctl run -t ubuntu

In both cases, Pods and VMs are indivisible. Hyper will automatically provision a new VM instance to host the Pod, and the Pod will be `Running`.

However, you can also create a Pod, but without an underlying VM. In such case, the pod stays in `Created` state.

    [root@user ~:]# hyperctl create -p podfile.json

There are two options to start the pod:

    [root@user ~:]# hyperctl start pod_id

The `START` command will trigger a VM provisioned, and allocate the new VM to the Pod.

When you `STOP` a Pod, the underlying VM instance will be terminated:

    [root@user ~:]# hyperctl stop pod_id

When stopped, the Pod will return to the `Created` state.

To permantly destroy a Pod, you need to `RM` it:

    [root@user ~:]# hyperctl rm pod_id

Hyper will (stop if neccessary, then) remove the Pod definition and its storage.
