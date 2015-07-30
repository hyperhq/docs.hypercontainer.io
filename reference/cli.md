# CLI

## Linux

```
Usage:

    hyper [OPTIONS] COMMAND [ARGS...]

Command:

    run         create a Pod, and launch a new VM to run the Pod
    start       launch a 'created' Pod in a VM
    stop        stop a running Pod and its VM
    exec        run a command in a container of a running Pod
    create      create a Pod, but without running it
    replace     replace the Pod in a running VM with a new one
    kill        terminate a VM instance
    rm          destory a Pod
    attach      attach to the tty of a specified container in a Pod
    pull        pull an image from a Docker registry server
    info        display system-wide information
    list        list all VMs, Pods or containers

Help Options:

   -h, --help  show this help message
```

## Mac OS X
```
Usage:

	hyper [OPTIONS] COMMAND [ARGS...]

Command:

    attach                 Attach to the tty of a specified container in a Pod
    build                  Build an image from a Dockerfile
    commit                 Create a new image from a container's changes
    create                 Create a Pod into 'pending' status, but without running it
    exec                   Run a command in a container of a running Pod
    images                 List images
    info                   Display system-wide information
    list                   List all Pods or containers
    login                  Register or log in to a Docker registry server
    logout                 Log out from a Docker registry server
    pull                   Pull an image from a Docker registry server
    push                   Push an image or a repository to a Docker registry server
    rm                     Remove one or more Pods
    rmi                    Remove one or more images
    run                    Create a Pod, and launch a new Pod
    start                  Launch a 'pending' Pod
    stop                   Stop a running Pod, it will become 'pending'

Help Options:

    -h, --help             Show this help message

Run 'hyper COMMAND --help' for more information on a command.
```
