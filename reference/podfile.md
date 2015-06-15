# Podfile

Podfile is in JSON format. A basic sample looks like the following:

    {
        "id": "myweb",
        "tty": true,

        "resource": {
            "vcpu": 1,
            "memory": "128"
        },

        "containers" : [{
            "image": "nginx:latest",
            "files":  [{
	            "path": "/var/lib/xxx/xxxx",
	            "filename": "filename",
	            "perm": "0755"
	        }]
        }],

        "files": [{
	        "name": "filename",
	        "encoding": "raw",
	        "uri": "https://s3.amazonaws/bucket/file.conf",
	        "content": ""
	    }],

        "volumes": []
    }

## Sections

- `id`: the identifier (and internal hostname) of the Pod
- `tty`: turn on/off (`true`/`false`) the tty connection to the Pod, default: `true`
- `resources`: specify the number of CPU cores and RAM size allocated to the HyperVM instance
- `containers`: a group of containers to run in the Pod
- `files`: files to be present in the containers
- `volumes`: volumes to mount from the host to the containers




