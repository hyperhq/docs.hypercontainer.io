# run

Create a pod, and launch the new pod

```
Usage:
  hyperctl run [OPTIONS] IMAGE [COMMAND] [ARG...]

Create and start a pod

Application Options:
  -p, --podfile=""       read spec from the pod file instead of command line
  -y, --yaml             pod file in Yaml format instead of JSON
      --name=""          Assign a name to the container
      --workdir=""       Working directory inside the container
  -t, --tty              the run command in tty, such as bash shell
      --cpu=1            CPU number for the VM (default: 1)
      --memory=128       Memory size (MB) for the VM (default: 128)
      --env=[]           Set environment variables
      --entrypoint=""    Overwrite the default ENTRYPOINT of the image
      --restart=""       Restart policy to apply when a container exits (never, onFailure, always) (default: never)
      --log-driver=""    Logging driver for Pod
      --log-opt=         Log driver options
      --publish=[]       Publish a container's port to the host, format: --publish [tcp/udp:]hostPort:containerPort
      --label=[]         Add labels for Pod, format: --label key=value
  -v, --volume=[]        Mount host file/directory as a data file/volume, format: -v|--volume=[[hostDir:]containerDir[:options]]
  -a, --attach           (from podfile) Attach the stdin, stdout and stderr to the container
  -d, --detach           (from cmdline) Not Attach the stdin, stdout and stderr to the container
      --rm               Automatically remove the pod when it exits

Help Options:
  -h, --help             Show this help message

Example:
	  hyperctl run -t ubuntu
	  hyperctl run -t ubuntu:latest
	  hyperctl run -t ubuntu /bin/bash
	  hyperctl run -d nginx
	  hyperctl run -p mypod.json
```
