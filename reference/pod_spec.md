# Hyper Pod specification

A Pod is described with json

## pod

- `name`: the identifier of the pod
- `containers`: the container to be run in dvm, described in correspond section.
- `files`: files would be written in one or more containers, described in correspond section.
- `volumes`: file or dir will be mapped into one or more containers, described in correspond section.
- `tty`: enable tty connection to pod, default: `true`

example:

    {
        "name": "hostname",
        "containers" : [{
            "image": "nginx:latest",
            "files":  [{
	            "path": "/var/lib/xxx/xxxx",
	            "filename": "filename"
	        }]
        }],
        "resource": {
            "vcpu": 1,
            "memory": "128"
        },
        "files": [{
	        "name": "filename",
	        "encoding": "raw", 
	        "uri": "https://s3.amazonaws/bucket/file.conf",
	        "content": ""
	    }],
        "volumes": [],
        "tty": true,
    }


## container

- `name`: identifier of a container in pod
- `image`: image name and tag of a image
- `ports`: public ports of containers
- `env`: environment for a container, the build-in envs are described in *environment variables* section
- `volumes`: volumes will be mount in the container, described in *volume* section
- `files`: files will be write in the container, described in *file* section
- `restartPolicy`: what to do if the container exit, `never`, `onFailure`, or `always`

example:

    {
        "name":  "app",
        "image": "repo/image:tag",
        "command": "",
        "entryPoint" [""],
        "ports": [{
            "containerPort": "4000",
            "hostPort": 0
        }],
        "envs":  [{
            "env": "JAVA_OPT",
            "value": "-XMx=256m"
        }],
        "volumes": [{
            "path": "/var/log",
            "volume": "name",
            "readOnly": false
        }],
        "files":  [
            "path": "/var/lib/xxx/xxxx",
            "filename": "name"
        ],
        "restartPolicy": "never"
    }

## file

File could be put into containers before running. Fields:

- `name`: identifier of the file
- `encoding`: file encoding, `raw` or `base64`, compressed or archive may be introduced in future version
- `uri`: accessible address of the file. if `content` is not provided, `uri` should not be empty.
- `content`: the (encoded) content of file. if `uri` is specified, the `content` field will be ignored.

example:

    {
        "name": "filename",
        "encoding": "raw", 
        "uri": "",
        "content": "contents string"
    }

## volume

- `name`: identifier of the volume
- `source`: path of the device, dir or file, or leave empty
- `driver`: 
  - block device: `raw`, `qcow2`
  - file or dir: `vfs`
  - distributed storage: tbd
  - empty: leave empty

example:

    {
        "name": ""
        "source": ""
        "driver": "vfs"
    }

## environment variables

pre-defined env variables:

- `DVM_POD_IP`: IP Address of the POD

