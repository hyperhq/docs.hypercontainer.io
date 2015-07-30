# build

Build a new image from the source code at PATH

(This command is only available on Mac OS X version)

```
Usage:
	hyper build [OPTIONS] PATH

Application Options:
	-t, --tag=""     Repository name (and optionally a tag) to be applied to the resulting image in case of success
	-f, --file=""    Customized docker file

Help Options:
	-h, --help       Show this help message

Example:
	hyper build -t test /dockerfile/path/
```
