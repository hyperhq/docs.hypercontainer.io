# Lifecycle

![](https://trello-attachments.s3.amazonaws.com/5562ba47387906ddef327e00/704x249/e4b1ec0168197c13e838bd5b405b3f28/pod.png)

In Hyper, a pod has two states:

- `Created`: a pod is defined, its storage has been allocated, and the Docker images have been downloaded
- `Running`: a pod (with its containers) is launched in a VM instance


A pod can be launched either explicitly:

	[root@user ~:]# hyper run -p podfile.json

Or, implicitly:

	[root@user ~:]# hyper run ubuntu /bin/sh

In both cases, pod and VM are inseverable. Hyper will automatically provision a new VM instance to host the pod, and the pod will be `Running`.

However, you can also create a pod, but without an underlying VM. In such case, the pod stays in `Created` state.

    [root@user ~:]# hyper create -p podfile.json

There are two options to start the pod:

    [root@user ~:]# hyper start pod_id

The `START` command will trigger a VM provisioned, and allocate the new VM to the pod. Alternatively, you can use `REPLACE` a running one:

    [root@user ~:]# hyper replace old_pod_id new_pod_id

In this case, the VM instance will be de-associated from `old_pod_id` and re-assign to `new_pod_id`. Since the VM is already present, `REPLACE` is a faster option to launch a pod, than `RUN` and `START`.

> Note: `old_pod_id` must be running.

When you `STOP` a pod, the underlying VM instance will be terminated:

    [root@user ~:]# hyper stop pod_id

When stopped, the pod will return to `Created`.

To permantly destroy a pod, you need to `RM` it:

    [root@user ~:]# hyper rm pod_id

Hyper will (stop if neccessary) remove the pod definition and its storage.
