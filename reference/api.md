# RESTful API

This is the REST API reference of `hyperd` based on [The latest release](../release_notes/latest.md).

### 1. Introduction
* By default `hyperd` listens on unix:///var/run/hyper.sock and the client must have root access to interact with the daemon.
* [The current release](../release_notes/latest.md) does not support encrypted connections.
* The Remote API uses an open schema model. In this model, unknown properties in incoming messages will be ignored. Client applications need to take this in consideration to ensure they will not break when talking to newer hyperd daemons.
* Calling `/info` is the same as calling `/${latest}/info`
* The API tends to be RESTful, but in a few exceptions, e.g. `attach`, `pull`, the HTTP connection is hijacked to transport stdout, stdin and stderr.

### 2. Endpoints
#### 2.1 Pod
##### Create Pod
`POST /pod/create`

Create a Pod

**Example request:**

`POST /pod/create?podArgs=****`

The argument is a string, which converts the Pod's json to a string.
##### Start Pod
`POST /pod/start`

Start a Pod

**Example request:**

`POST /pod/start?podId=pod-xxxxxxxxxx&vmId=vm-xxxxxxxxxx`

If the VM id is empty (""), then it will create a new VM.
##### Stop Pod
`POST /pod/stop`

Stop a Pod

**Example request:**

`POST /pod/stop?podId=pod-xxxxxxxxxx&stopVM=yes`

The `stopVM` property can be `yes` or `no`; it will destroy the VM associated with the Pod if its value is `yes`

##### Delete Pod
`DELETE /pod`

Destroy a Pod

**Example request:**

`DELETE /pod?podId=pod-xxxxxxxxxx`

##### List Pods
`GET /list`

List pods

**Example request:**

`GET /list?item=pod`

##### GET Pod info

`GET /pod/info`

Get Pod detail information

**Example request:**

`GET /pod/info?podId=pod-xxxxxxxxxx`

##### Get Pod Stats

`GET /pod/stats`

Get Pod stats info

**Example request:**

`GET /pod/stats?podId=pod-xxxxxxxxxx`

##### Set Pod label

`POST /pod/labels`

Set pod labels

**Example request:**

`POST /pod/labels?podId=pod-xxxxxxxxxx&labels={"ll":"vv"}&override=true`

##### Send Signal to Pod

`POST /pod/kill`

Send kill signal to containers of a Pod

**Example request:**

`POST /pod/kill?podName=pod-xxxxxxxxxx&container=xxxxxxx&signal=9`

##### List Port Mapping Rules

`GET /pod/{pod_id}/portmappings`

Get a list of current port mappings of a pod.

##### Modify Port Mapping Rules

`PUT /pod/{pod_id}/portmappings/{action}`

Update port mapping rules

- `action` could be `add` or `delete`

The request body is an json **array** of `PortMapping`:

```
{
	"containerPort": "80",
	"hostPort": "3000",
	"protocol": "udp"
}
```

Where

- `containerPort` and `hostPort` could be a single port or a range, such as "8000-8080"; and if the `containerPort` is a range, the `hostPort` should be a range in same size;
- `protocol` could be `tcp` or `udp`.

The request body should be an array even if there is only one rule to be added/deleted.

#### 2.2 Container
##### Create container
`POST /container/create`

Create a container

**Example request:**

`POST /pod/create`

The body is a [container spec in JSON format](./containers.md).

##### Start container

`POST /container/start`

Start a container

**Example request:**

`POST /container/start?container=xxxxxxxx`

##### Stop container

`POST /container/stop`

Stop a container

**Example request:**

`POST /container/stop?container=xxxxxxxx`

##### Kill container

`POST /container/kill`

Kill a container with a signal

**Example request:**

`POST /container/kill?container=xxxxxxxx&signal=9`

##### Delete container

`POST /container/remove`

Remove a container from Pod

**Example request:**

`POST /container/remove?container=xxxxxxxx`

##### Rename container

`POST /container/rename`

Rename a container

**Example request:**

`POST /container/rename?newName=yyyyyyy&oleName=xxxxxxxx`

##### List containers
`GET /list`

List containers

**Example request:**

`GET /list?item=container`

##### Get container info

`GET /container/info`

Get container info

**Example request:**

`GET /container/info?container=xxxxxxxx`

##### Get container logs

`GET /container/logs`

Get container logs

**Example request:**

`GET /container/logs?container=xxxxxxxx&stdout=true&stderr=true&follow=false&timestamp=true&tail=100`

##### Get container or exec exit code

`GET /container/exitcode`

**Example request:**

`GET /container/exitcode?container=xxxxxxxx&exec=eeeeeeeee`

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

#### 2.3 Attach and Exec

##### Attach to container

`POST /attach`

Attach to a container, will upgrade to TCP stream.

##### TTY resize

`POST /tty/resize`

Change the tty window size of container or exec

**Example request:**

`POST /tty/resize?container=xxxxxxxx&exec=eeeeeeeee&h=25&w=80`

##### Create exec

`POST /exec/create`

Create an exec

**Example request:**

`POST /exec/create?container=xxxxxxxx&tty=true&command=/bin/bash`

##### Start exec

`POST /exec/start`

Start an exec

**Example request:**

`POST /exec/start?container=xxxxxxxx&exec=eeeeeeeee`

The exec request will upgrade to TCP stream

#### 2.4 Info
##### System-wide info
`GET /info`

Display system-wide information

**Example request:**

`GET /info`

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

##### Create or pull an image
`POST /image/create`

Create an image, either by pulling it from the registry or by importing it

**Example request:**

`POST /image/create?imageName=ubuntu HTTP/1.1`

**Example response:**
```
    HTTP/1.1 200 OK
    Content-Type: application/json

    {"status": "Pulling..."}
    {"status": "Pulling", "progress": "1 B/ 100 B", "progressDetail": {"current": 1, "total": 100}}
    {"error": "Invalid..."}
    ...

When using this endpoint to pull an image from the registry, the
`X-Registry-Auth` header can be used to include
a base64-encoded AuthConfig object.
```

Query Parameters:

```
imageName – name of the image to pull

Request Headers:
X-Registry-Auth – base64-encoded AuthConfig object
```

##### Remove an image
`DELETE /image`

Remove an image

**Example request:**

`DELETE /image?imageId=xxxxxxxxxxxx`

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
