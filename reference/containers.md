# Container Spec

- `name`: the identifier of a container; a random id will be given if absent

- `image`: in the form `[registry]/image[:tag]`; hyperctl will automatically pull the image if missing

- `command`: the shell command to run when the container starts

- `entryPoint`: the executable to run when the container starts
    - The `command` will be appended to `entryPoint` as parameters if `entryPoint` is not empty.

- `workdir`: the directory running the container command

- `ports`: the exposed ports of the container
    - `containerPort`: the listening port inside container
    - `hostPort`: the port exposed in host machine
    - `protocol`: `tcp` (default) or `udp`

- `volumes`: volumes reference to be mounted in the container.
    -  `path`: the mount point
    -  `volume`: the name of the volume to be mounted, defined in [volumes](./volumes.md) section, or specified in `detail`.
    -  `readOnly`: if `true`, the mount point will be read only, default `false`
    -  `detail`: the [volume spec](./volumes.md). If the volume is defined in `volumes` section of the pod, the `detail` field could leave null.

- `files`: files reference to be present in the container
    -  `path`: the file path in the container
    -  `filename`: the filename defined in [files](./files.md) section, or specified in `detail`.
    -  `perm`: the file permission, by default `0755`
    -  `detail`: the [file spec](./files.md). If the file is defined in `files` section of the pod, the `detail` field could leave null.

- `tty`: whether the stdio of the container is a tty device

example:

    "containers" : [{
        "id":  "app",
        "image": "repo/image:tag",
        "command": ["/bin/sh"],
        "workdir": "/root",
        "envs":  [{
            "env": "JAVA_OPT",
            "value": "-XMx=256m"
        }],
        "volumes": [{
            "path": "/var/log",
            "volume": "name",
            "readOnly": false,
            "detail": {                             
                      "name": "prod_log",
                      "source": "/var/log/myweb.img",
                      "format": "raw"
          	}
        }],
        "files":  [{
            "path": "/var/lib/xxx/xxxx",
            "filename": "name",
            "perm": "0755",
            "detail": {
    	        "name": "nginx.conf",
    	        "encoding": "raw",
    	        "uri": "https://s3.amazonaws/bucket/file.conf",
    	        "content": ""
    	    }
        }],
        "ports":[{
            "containerPort": 80,
            "hostPort": 8000,
        }],
        "tty": true
    }]
