# run

You can run only `hyper run -p POD_FILE` or `hyper run ubuntu bash` to start a Pod and VM.

If needed, you can add the following options:

	Usage:
	  hyper run [OPTIONS] IMAGE [COMMAND] [ARG...]

	Application Options:
	  -p, --podfile=""       Create and Run a Pod based on the Pod file
	  -n, --name=""          Assign a name to the container
	  -a, --attach           Attach stdin, stdout and stderr to the container
	  -w, --workdir=""       Working directory inside the container
	  -t, --tty              Allocate a pseudo-TTY
	  -c, --cpu=1            CPU shares (relative weight)
	  -m, --memory=128       Memory limit (format: <number><optional unit>; where unit = b, k, m or g)
	  -e, --env=[]           Set environment variables
	      --entrypoint=""    Overwrite the default ENTRYPOINT of the image
	  -r, --restart=""       Restart policy to apply when a container exits (no, on-failure[:max-retry], always)

	Help Options:
	  -h, --help             Show this help message
