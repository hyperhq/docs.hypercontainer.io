# Files

Besides map a local file to container via [`volumes`](./volumes.md), Hyper allows you to insert new files into containers in a HyperVM instance. The content of the inserted file could be specified in Pod or get from a URL. To do this, simply define the files to be attached in `files` section, and reference the `filename` in `container` section:

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
	            "path": "/etc/",
	            "filename": "nginx.conf",                      # Reference here
	            "perm": "0755"
	        }]
        }],

        "files": [{                                                 # Definition
	        "name": "nginx.conf",
	        "encoding": "raw",
	        "uri": "https://s3.amazonaws/bucket/file.conf",
	        "content": ""
	    }]
    }


The `files` section is a list of items with the following properties:
- `name`: the file name; used in **Section 'Containers'**

- `encoding`: the file encoding; `raw` or `base64`. the content will be decoded when `base64` is specified

- `uri`: fetch the file from this address, could be either a net url such as `http://example.com/myfile` or local file with `file:///`

- `content`: specify the content of the file

> One file can be shared by multiple containers in a Pod with different `path` and `perm`. Therefore, any changes to the file content will be visible across the entire Pod.
