# Volumes

Similar with Docker, Hyper allows you to mount additional volumes to a HyperVM instance. To do this, simply define the volumes to be attached in `volumes` section, and reference the `volume` in `container` section:

    {
        "name": "myweb",
        "tty": true,

        "resource": {
            "vcpu": 1,
            "memory": "128"
        },

        "containers" : [{
            "image": "nginx:latest",
            "volumes": [{                           # Reference here
                "volume": "prod_log",
                "path": "/var/log",
                "readOnly": false
             }]
        }],

    	"volumes": [{                               # Definition
                "name": "prod_log",
                "source": "/var/log/myweb.img",
                "driver": "qcow2"
    	}],
    }


The `volumes` section is a list of items with the following properties:

- `name`: identifier of the volume
- `source`: the volume path on the host, either directory or file. If absent, a new 10GB volume will be created
- `driver`: the volume format
  - block-device-image file: `raw`, `qcow2`, this allows to mount a VM image to HyperVM. Note: the image file must have a `EXT4` fs in it.
  - plain file or dir: `vfs`, this options is to mount a file/dir on the host to to HyperVM instance
  - empty: leave empty

> One volume can be mounted in multiple containers in a pod with different `path` and `readOnly` properties. Therefore, any data change in the volume will be visible across the entire Pod.
