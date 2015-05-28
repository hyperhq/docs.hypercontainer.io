# replace

<<<<<<< HEAD
Deallocate the VM instance from a `Running` pod A and re-assign to a `Pending` pod B. Pod A will return to `Pending`
=======
Deallocate the VM instance from a `Running` Pod A and re-assign to a `Pending` Pod B. Pod A will return to `Pending` state
>>>>>>> f70b1f92db92d3a5d9b40f3ccdf29a685e42f4a2

	Usage:
	  hyper replace --oldpod POD_ID --newpod POD_ID [--file POD_FILE]

	Application Options:
	  -o, --oldpod=""    The Pod that will be replaced, must be in 'running' status
	  -n, --newpod=""    The Pod that will be run, must be in 'created' status
	  -f, --file=""      The Pod file to use to create and run the new Pod

	Help Options:
	  -h, --help         Show this help message
