# exec

Run a command in a container or a Pod, and attach the current terminal to the command stdio.

```
Usage:
  hyperctl exec [OPTIONS] POD|CONTAINER COMMAND [ARGS...]

Run a command in a container or a Pod

Application Options:
  -d, --detach  Not Attach the stdin, stdout and stderr to the process
  -t, --tty     Allocate a pseudo-TTY
  -m, --vm      Execute outside of any containers

Help Options:
  -h, --help    Show this help message
```
