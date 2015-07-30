# Files

Hyper allows you to attach additional files to a HyperVM instance. To do this, simply define the files to be attached in `files` section, and reference the `filename` in `container` section:

    {
        "name": "myweb",
        "tty": true,

        "resource": {
            "vcpu": 1,
            "memory": "128"
        },

        "containers" : [{
            "image": "nginx:latest",
            "files":  [{
	            "path": "/etc/nginx.conf",
	            "filename": "prod_nginx.conf",                      # Reference here
	            "perm": "0755"
	        }]
        }],

        "files": [{                                                 # Definition
	        "name": "prod_config.conf",
	        "encoding": "raw",
	        "uri": "https://s3.amazonaws/bucket/file.conf",
	        "content": ""
	    }]
    }


The `files` section is a list of items with the following properties:
- `name`: the file name; used in **Section 'Containers'**

- `encoding`: the file encoding; `raw` or `base64`. the content will be decoded when `base64` is specified

- `uri`: fetch the file from this address

- `content`: specify the content of the file

> One file can be shared by multiple containers in a Pod with different `path` and `perm`. Therefore, any changes to the file content will be visible across the entire Pod.
