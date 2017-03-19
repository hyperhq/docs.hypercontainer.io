# Pod Spec

Podfile is in JSON format. A basic sample looks like the following:

    {
        "id": "myweb",
        "hostname": "myname",
        "resource": {
            "vcpu": 1,
            "memory": 128
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
- `hostname`: the hostname of the Pod
- `resources`: specify the number of CPU cores and RAM size allocated to the HyperVM instance
- `containers`: a group of [containers](./containers.md) to run in the Pod. Since 0.8, we could create a Pod with empty containers list, and add containers later.
- `files`: [files](./files.md) to be present in the containers
- `volumes`: [volumes](./volumes.md) to mount from the host to the containers
