# build

Build a new image from the source code at PATH

```
Usage:
	hyperctl build [OPTIONS] PATH

Application Options:
	-t, --tag=""     Repository name (and optionally a tag) to be applied to the resulting image in case of success
	-f, --file=""    Customized docker file

Help Options:
	-h, --help       Show this help message

Example:
	hyperctl build -t test /dockerfile/path/
```
