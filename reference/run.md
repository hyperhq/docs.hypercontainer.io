# run

<<<<<<< HEAD
Launch one or multiple Docker images as a pod, with a new VM instance
=======
Launch one or multiple Docker images as a Pod, with a new VM instance
>>>>>>> f70b1f92db92d3a5d9b40f3ccdf29a685e42f4a2

	Usage:
	  hyper run [OPTIONS] IMAGE [COMMAND] [ARG...]

	Application Options:
	  -p, --podfile=""       Create and Run a Pod based on the Pod file
	  -n, --name=""          Assign a name to the container
	  -a, --attach           Attach stdin, stdout and stderr to the container
	  -w, --workdir=""       Working directory inside the container
	  -t, --tty              Allocate a pseudo-TTY
	  -c, --cpu=1            Number of CPU cores
	  -m, --memory=128       Memory limit (format: <number><optional unit>; where unit = b, k, m or g)
	  -e, --env=[]           Set environment variables
	      --entrypoint=""    Overwrite the default ENTRYPOINT of the image
	  -r, --restart=""       Restart policy to apply when a container exits (no, on-failure[:max-retry], always)

	Help Options:
	  -h, --help             Show this help message

	Example:
	  hyper run ubuntu
	  hyper run ubuntu:latest
	  hyper run ubuntu /bin/sh
	  hyper run -p mypod.json


