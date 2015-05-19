
## States

### VM

VM is a running VM process, a Pod could run on top of a vm, and stop on it, and VM does not has persistent status, will be reclaim after shutdown.

A running VM has 2 state:

- **Associated** with a Pod, or
- **Idle**

### Pod

A pod is the atomic unit to schedule with, contains one or more containers, which is an instance of a Image.

A pod is specified by a *Pod spec*, and has persistent data after being created, and won't be removed from storage until being removed explicitly.

A pod has the following states

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

Common procedures could change VM or Pod status, or just change one of them.

- **run-pod** (short as **pod**)
  - run a VM, create a Pod, and let the pod run on the VM
  - if has VM-id parameter, could run pod on an exist vm
  - if pod enabled tty and specified in command line, will attach to the tty of an container
- **run-vm** (short as **vm**)
  - run a VM, without any Pod running on it
- **create-pod** (short as **create**)
  - create a pod, let a pod become created but not run it
- **start-pod** (short as **start**)
  - run a created Pod in a VM, create VM if VM id is not provided
- **stop-pod** (short as **stop**)
  - stop a Pod and VM it's running on
  - if has flag, will stop pod only, leave vm running
- **replace-pod** (short as **replace**)
  - stop a running pod on a , (create and )start another pod on the VM
  - create and start is the default behavior, not create if a existing pod id provided
- **attach** attach to tty of a specified container in a pod
- **exec** 
  - run a command in a container in a pod, and attach current terminal to the stdio of oommand
  - do not attach if detached flag (`-d`) provided


### Infomative Commonds

- **info** daemon configuration, like docker info
- **list** list exist vm, pod, and containers

### Short cut

- **run**, run a container on a VM and 

### Bridge to docker

- **pull**, pull docker image from registry to local