# API

This is the API reference of `hyperd` based on [The latest release](../release_notes/latest.md).


### 1. Introduction
* By default `hyperd` listens on unix:///var/run/hyper.sock and the client must have root access to interact with the daemon.
* [The current release](../release_notes/latest.md) does not support encrypted connections.
* The Remote API uses an open schema model. In this model, unknown properties in incoming messages will be ignored. Client applications need to take this in consideration to ensure they will not break when talking to newer hyperd daemons.
* Calling `/info` is the same as calling `/${latest}/info`
* The API tends to be RESTfull, but for some complex commands, like attach or pull, the HTTP connection is hijacked to transport stdout, stdin and stderr

### 2. Endpoints
#### 2.1 Pod
##### Create pod
`POST /pod/create`

Create a pod

**Example request:**

`POST /pod/create?podArgs=****`

The argument is a string, which converts the pod's json to a string.
##### Start pod
`POST /pod/start`

Start a pod

**Example request:**

`POST /pod/start?podId=pod-xxxxxxxxxx&vmId=vm-xxxxxxxxxx`

If the VM id is empty (""), then it will create a new VM.
##### Stop pod
`POST /pod/stop`

Stop a pod

**Example request:**

`POST /pod/stop?podId=pod-xxxxxxxxxx&stopVM=yes`

The `stopVM` property can be `yes` or `no`; it will destroy the VM associated with the pod if its value is `yes`

##### Destroy pod
`POST /pod/remove`

Destroy a pod

**Example request:**

`POST /pod/remove?podId=pod-xxxxxxxxxx`


##### List pods
`GET /list`

List pods

**Example request:**

`GET /list?item=pod`

#### 2.2 Container
##### List containers
`GET /list`

List containers

**Example request:**

`GET /list?item=container`

##### Create a new image from a container’s changes
`POST /container/commit`

**Example request:**

```
	POST /container/commit?container=44c004db4b17&comment=message&repo=myrepo HTTP/1.1
    Content-Type: application/json

    {
         "Hostname": "",
         "Domainname": "",
         "User": "",
         "Memory": 0,
         "MemorySwap": 0,
         "CpuShares": 512,
         "Cpuset": "0,1",
         "AttachStdin": false,
         "AttachStdout": true,
         "AttachStderr": true,
         "PortSpecs": null,
         "Tty": false,
         "OpenStdin": false,
         "StdinOnce": false,
         "Env": null,
         "Cmd": [
                 "date"
         ],
         "Volumes": {
                 "/tmp": {}
         },
         "WorkingDir": "",
         "NetworkDisabled": false,
         "ExposedPorts": {
                 "22/tcp": {}
         }
    }
```

#### 2.3 Info
##### System-wide info
`GET /info`

Display system-wide information

**Example request:**

`GET /info`

#### 2.4 VM
##### Create VM
`POST /vm/create`

Create a VM

**Example request:**

`POST /vm/create`

##### Kill VM
`POST /vm/kill`

Kill a VM

**Example request:**

`POST /vm/kill?vm=vm-xxxxxxxxxx`

##### List VMs
`GET /list`

List all VMs

**Example request:**

`GET /list?item=vm`

#### 2.5 Images
##### List Images
`GET /images/get`

Get images' list

**Example request:**

`GET /images/get?all=yes`

Query Parameters:

```
all – yes or no, default no
```

##### Remove an image
`POST /images/remove`

Remove an image

**Example request:**

`POST /images/remove?imageId=xxxxxxxxxxxx`

Query Parameters:

```
force – yes or no, default no
noprune – yes or no, default no
```

##### Build an image from a Dockerfile
`POST /image/build`

**Example request:**

```
    POST /image/build HTTP/1.1

    {{ TAR STREAM }}
```

The input stream must be a tar archive compressed with one of the following algorithms: identity (no compression), gzip, bzip2, xz.

The archive must include a build instructions file, typically called `Dockerfile` at the root of the archive. The `dockerfile` parameter may be used to specify a different build instructions file by having its value be the path to the alternate build instructions file to use.

The archive may include any number of other files, which will be accessible in the build context.

Query Parameters:

```
dockerfile - path within the build context to the Dockerfile
t          – repository name (and optionally a tag) to be applied to the resulting image in case of success
remote     – git or HTTP/HTTPS URI build source
q          – suppress verbose build output
nocache    – do not use the cache when building the image
pull       - attempt to pull the image even if an older image exists locally
rm         - remove intermediate containers after a successful build (default behavior)
forcerm    - always remove intermediate containers (includes rm)
```
Request Headers:

```
Content-type      – should be set to "application/tar".

X-Registry-Config – base64-encoded ConfigFile object
```

##### Push an image on the registry
`POST /image/push`

Push the image on the registry

**Example request:**

`POST /images/push?remote=test`

Query Parameters:

```
remote - the image on the registry
tag    – the tag to associate with the image on the registry, optional
```

Request Headers:

```
X-Registry-Auth – include a base64-encoded AuthConfig object.
```

#### 2.6 Auth
`POST /auth`

Get the default username and email

**Example request:**

```
	POST /auth HTTP/1.1
	Content-Type: application/json

	{
    	"username":"hello",
    	"password: "world",
    	"email": "hellol@a-team.com",
    	"serveraddress": "https://index.docker.io/v1/"
	}
```

