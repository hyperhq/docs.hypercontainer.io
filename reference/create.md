# create

Create a pod or create a container in a pod.

```
Usage:
  hyperctl create [OPTIONS] [POD_ID] IMAGE [COMMAND] [ARG...]

Create a pod, or create a container in the pod specified by the POD_ID

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
  -c, --container        Create container inside a pod

Help Options:
  -h, --help             Show this help message
```
