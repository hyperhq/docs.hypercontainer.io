# exec

Run a command in a container or a Pod, and attach the current terminal to the stdio of this command

	Usage:
	  hyper exec POD_ID:CONTAINER_NAME COMMAND [ARGS...]

	Help Options:
	  -h, --help            Show this help message

    Example:
      hyper exec pod-3uhg23po:nginx echo "Hello World"
