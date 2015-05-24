# API

This is the API reference of `hyperd` based on [The latest release](../release_notes/latest.md).


### 1. Introduction
* By default `hyperd` listens on unix:///var/run/hyper.sock and the client must have root access to interact with the daemon.
* [The current release](../release_notes/latest.md) does not support an encrypted connection.
* The Remote API uses an open schema model. In this model, unknown properties in incoming messages will be ignored. Client applications need to take this into account to ensure they will not break when talking to newer hyperd daemons.
* Calling `/info` is the same as calling `/${latest}/info`
* The API tends to be REST, but for some complex commands, like attach or pull, the HTTP connection is hijacked to transport stdout stdin and stderr

### 2. Endpoints
#### 2.1 Pod
##### Create pod
`POST /pod/create`

Create a pod

**Example request:**

`POST /pod/create?podArgs=****`

The argument is a string which convert the user pod's json to string.
##### Start pod
`POST /pod/start`

Start a pod

**Example request:**

`POST /pod/start?podId=pod-xxxxxxxxxx&vmId=vm-xxxxxxxxxx`

The VM id can be "", and then it will create a new VM.
##### Stop pod
`POST /pod/start`

Stop a pod

**Example request:**

`POST /pod/stop?podId=pod-xxxxxxxxxx&stopVM=yes`

The `stopVM` property can be `yes` or `no`, it will desctroy the VM associated with the pod if its value is `yes`

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

#### 2.2 Info
##### System-wide info
`GET /info`

Display system-wide information

**Example request:**

`GET /info`

#### 2.2 VM
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
