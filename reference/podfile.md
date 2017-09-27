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
        "portmappings": [{
          "containerPort": "80",
          "hostPort": "3000",
          "protocol": "udp"
	      }],
        "volumes": []
    }

## Sections

- `id`: the identifier (and internal hostname) of the Pod
- `hostname`: the hostname of the Pod
- `resources`: specify the number of CPU cores and RAM size allocated to the HyperVM instance
- `containers`: a group of [containers](./containers.md) to run in the Pod. Since 0.8, we could create a Pod with empty containers list, and add containers later.
- `portmappings`: the port mapping rules, and the portmappings could be `add`/`remove` during runtime with API or command line tools. The fields:
  - `containerPort` and `hostPort` could be a single port or a range, such as "8000-8080"; and if the `containerPort` is a range, the `hostPort` should be a range in same size;
  - `protocol` could be `tcp` or `udp`.
- `files`: [files](./files.md) to be present in the containers
- `volumes`: [volumes](./volumes.md) to mount from the host to the containers
