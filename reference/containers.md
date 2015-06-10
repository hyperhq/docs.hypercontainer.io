# Containers

- `name`: the identifier of a container; a random id will be given if absent

- `image`: in the form `[registry]/image[:tag]`; hyper will automatically pull the image if missing

- `command`: the shell command to run when the container starts

- `entryPoint`: the executable to run when the container starts (override `command`)

- `ports`: the exposed ports of the container **(RESERVED)**

- `envs`: set a list of environment variables in the container
    - (*Predefined*) `HYPER_POD_IP`: IP Address of the Pod

- `volumes`: volumes to be mounted in the container.
    -  `path`: the mount point
    -  `volume`: the name of the volume to be mounted, defined in [volumes](./volumes.md) section
    -  `readOnly`: if `true`, the mount point will be read only, default `false`

- `files`: files to be present in the container
    -  `path`: the file path in the container
    -  `filename`: the filename defined in [files](./files.md) section
    -  `perm`: the file permission, by default `0755`

- `restartPolicy`: restart the container if exit: `never`, `onFailure`, or `always`

example:

    "containers" : [{
        "name":  "app",
        "image": "repo/image:tag",
        "command": ["/bin/sh"],
        "entryPoint" [""],
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
            "filename": "name",
            "perm": "0755"
        ],
        "restartPolicy": "never"
    }]
