# run

Launch one or multiple Docker images as a Pod, with a new VM instance

    Usage:
      hyper run [OPTIONS] IMAGE [COMMAND] [ARG...]

    Create a pod, and launch a new VM to run the pod

    Application Options:
      -p, --podfile=""       Create and Run a pod based on the pod file
      -k, --kubernetes=""    Create and Run a pod based on the kubernetes pod file
      -y, --yaml             Create a pod based on Yaml file
          --name=""          Assign a name to the container
      -a, --attach           (from podfile) Attach the stdin, stdout and stderr to the container
      -d, --detach           (from cmdline) Not Attach the stdin, stdout and stderr to the container
          --workdir=""       Working directory inside the container
      -t, --tty              the run command in tty, such as bash shell
          --cpu=1            CPU number for the VM
          --memory=128       Memory size (MB) for the VM
          --env=[]           Set environment variables
          --entrypoint=""    Overwrite the default ENTRYPOINT of the image
          --restart=""       Restart policy to apply when a container exits (never, onFailure, always)
          --log-driver=""    Logging driver for Pod
          --log-opt=         Log driver options
          --rm               Automatically remove the pod when it exits
          --publish=[]       Publish a container's port to the host, format: --publish [tcp/udp:]hostPort:containerPort

    Help Options:
      -h, --help             Show this help message

	Example:
	  hyper run -t ubuntu
	  hyper run -t ubuntu:latest
	  hyper run -t ubuntu /bin/bash
	  hyper run -d nginx
	  hyper run -p mypod.json


