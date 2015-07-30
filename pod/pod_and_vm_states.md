
# The Life of Pod

### Pod

A Pod is the atomic unit to schedule, containing one or more containers, which are instances of an Image.

A Pod is specified by a *Pod spec*, and has persistent data after being created, and won't be removed from storage until being removed explicitly.

A Pod has the following states

- **None**: No ID, No storage, Noting at all
- **Created**: Prepared, but not run
  - Container storage allocated, but
    - for dm, only stay in thin pool, do not make device in `/dev`
    - for aufs, dir created and file putted, do not mount aufs in anywhere
  - Volume only allocated, like container
- **Running**: Running on a VM, could attach to and exec command in container
  - Container and Volume device inserted to VM, or dirs bound/mounted in correspond path

## Procedures & Commands

### Common Procedures

Common procedures can change the VM or Pod status

- **run-pod** (shorten as **pod**)
  - run a VM, create a Pod, and let the pod run on the VM
  - if has VM-id parameter, could run pod on an existing VM
  - if Pod tty is enabled, and specified in command line, will attach to the tty of a container
- **run-vm** (shorten as **vm**)
  - run a VM, without any Pod running on it
- **create-pod** (shorten as **create**)
  - create a pod, let a pod become created but not run it
- **start-pod** (shorten as **start**)
  - run a created Pod in a VM, create VM if VM id is not provided
- **stop-pod** (shorten as **stop**)
  - stop a Pod and its VM running on
  - if has "flag", will stop Pod only, leaving VM running
- **replace-pod** (shorten as **replace**)
  - stop a running Pod, then (create and) start another Pod on the VM
  - create and start is the default behavior, do not create if an existing Pod id provided
- **attach** attach to tty of a specified container in a Pod
- **exec**
  - run a command in a container, within a Pod, and attach the current terminal to the stdio of command
  - do not attach if detached flag (`-d`) is provided


### Informative Commands

- **info** daemon configuration, like `docker info`
- **list** list existing VMs, Pods, and Containers

### Shortcut

- **run**, run a container on a VM

### Bridge to docker

- **pull**, pull docker image from remote registry to local
