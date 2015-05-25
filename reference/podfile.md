# Podfile

Podfile is in JSON format. A basic sample looks like the following:

    {
        "name": "myweb",
        "containers" : [{
            "image": "nginx:latest",
            "files":  [{
	            "path": "/var/lib/xxx/xxxx",
	            "filename": "filename",
	            "permission":
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

## Sections

- `name`: the identifier (and internal hostname) of the pod
- `containers`: a group of containers to run in the pod
- `files`: files to be present in the containers
- `volumes`: volumes to mount from the host to the containers
- `tty`: turn on/off (`true`/`false`) the tty connection to the pod, default: `true`

> ### Containers

- `name`: the identifier of a container; a random id will be given if absent

- `image`: in the form `[registry]/image[:tag]`; hyper will automatically pull the image if missing

- `command`: the shell command to run when the container starts

- `entryPoint`: the executable to run when the container starts (override `command`)

- `ports`: the exposed ports of the container **(RESERVED)**

- `envs`: set a list of environment variables in the container
    - (*Predefined*) `HYPER_POD_IP`: IP Address of the POD

- `volumes`: volumes to be mounted in the container.
    -  `path`: the mount point
    -  `volume`: the name of the volume to be mounted, defined in **Section 'Volumes'**
    -  `readOnly`: if `true`, the mount point will be read only, default `false`

- `files`: files to be present in the container
    -  `path`: the file path in the container
    -  `filename`: the filename defined in the **Section 'Files'**

- `restartPolicy`: restart the container if exit: `never`, `onFailure`, or `always`

example:

    "containers" : [{
        "name":  "app",
        "image": "repo/image:tag",
        "command": "/bin/sh",
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
    }]

> ### Files

- `name`: the file name; used in **Section 'Containers'**

- `encoding`: the file encoding; `raw` or `base64`. the content will be decoded when `base64` is specified

- `uri`: fetch the file from this address

- `content`: specify the content of the file

example:

    {
        "name": "filename",
        "encoding": "raw",
        "uri": "",
        "content": "Hellow World"
    }

> ### Volumes

- `name`: identifier of the volume

- `source`: the volume path on the host, either directory or file. If absent, a new volume will be created

- `driver`: the volume format
  - block-device-image file: `raw`, `qcow2`, the image file must contain `EXT4` fs
  - plain file or dir: `vfs`
  - empty: leave empty

example:

    {
        "name": ""
        "source": ""
        "driver": "vfs"
    }



