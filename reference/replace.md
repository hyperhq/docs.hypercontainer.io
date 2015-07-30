# replace

Deallocate the VM instance from a `Running` Pod A and re-assign to a `Created` Pod B. Pod A will return to `Created` state

(This command is only avaiable for Linux version)

	Usage:
	  hyper replace --oldpod POD_ID --newpod POD_ID [--file POD_FILE]

	Application Options:
	  -o, --oldpod=""    The Pod that will be replaced, must be in 'running' status
	  -n, --newpod=""    The Pod that will be run, must be in 'created' status
	  -f, --file=""      The Pod file to use to create and run the new Pod

	Help Options:
	  -h, --help         Show this help message
