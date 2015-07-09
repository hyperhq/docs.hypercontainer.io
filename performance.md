# Performance

## 1. Time


### 1.1 Pod startup time

Run a new Pod only takes `376` millisecond (ms).

| - | with-qboot | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- | --- |
| hyper for kvm | yes | 352 | 391 | 376 |
| hyper for kvm | no | 685 | 725 | 709 |
| hyper for qemu | yes | 1348 | 1380 | 1367 |
| hyper for qemu | no | 1773 | 1809 | 1787 |
| hyper for xen | no | 2426 | 2486 | 2449 |



### 1.2 Pod replace time

Replace a running Pod with a new one, only takes `150` ms.

| -   | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- |
| replace time | 128 | 171 | 150 |


## 2. Density Test

Create VM/pod ceaselessly, until "Cannot allocate memory" occurs.

### 2.1 Test environment

  - Total of physical memory  
  	`16`GB
  - Allocation of resources  
  	`1` vCPU, `512`MB Memory
  - Test Docker image  
  	ubuntu:14.04 - https://registry.hub.docker.com/_/ubuntu/
  - Test KVM image  
  	http://cloud-images.ubuntu.com/releases/14.04/release-20150706/ubuntu-14.04-server-cloudimg-amd64-disk1.img


### 2.2 Result

In the same condition, Hyper can run more Pods than traditional VMs, and there is more available memory for user's applications.

#### 2.2.1 Traditional VM(kvm)

Max VM(KVM) number : `105`

> **QEMU process memory usage**(MB): (105 qemu processes)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    70 |   184 |   `156` |
|VSZ(VmSize)|   928 |   928 |   928 |

> **memory usage in VM** (MB): (105 running VMs)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   490 |   490 |   490 |
|Used |    342 |    344 |    `343` |
|Free |   145 |   147 |   `146` |


#### 2.2.2 Hyper pod

Max Pod(Hyper) number : `252`

> **QEMU process memory usage**(MB): (252 qemu processes)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    61 |    75 |    `69` |
|VSZ(VmSize)|   994 |  1066 |   995 |

> **memory usage in Pod** (MB): (252 running Hyper Pods)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   498 |   498 |   498 |
|Used |    14 |    14 |    `14` |
|Free |   484 |   484 |   `484` |


## 3. Memory Utilization

### 3.1 Minimum startup memory

The minimum startup memory is `28`(MB)


### 3.2 QEMU process memory usage

When starting a Pod with minimum startup memory, QEMU process uses `50`MB of the host OS' physical memory.

|  -  | min(MB) | max(MB) | avg(MB) |
| --- | --- | --- | --- |
|RSS(VmRSS) |    49 |    53 |    50 |
|VSZ(VmSize)|   510 |   582 |   512 |


### 3.3 Memory usage in Pod

When starting a Pod with minimum startup memory, there will be `6`MB of available memory in a running Pod. Hyper Kernel only takes `13`MB of memory.

|  -  | min(MB) | max(MB) | avg(MB) |
| --- | --- | --- | --- |
|Total|    19 |    19 |    19 |
|Used |    13 |    13 |    13 |
|Free |     6 |    6 |     6 |



## 4. CPU Performance

Allocation of resources: `1` vCPU, `2048`MB of Memory

The following table is the result of `dhrystone` CPU performance test.

| - | DMIPS(avg) |
| --- | --- |
| host | 24938 |
| docker | 24875 |
| hyper | 24817 |

> In the target column,  `host` means Host OS, `docker` means Docker container, `hyper` means Hyper Pod


The following table is the result of `whetstone` CPU performance test.

| - | MFLOPS(avg) |
| --- | --- |
| host | 5064 |
| docker | 5056 |
| hyper | 5050 |



## 5. Memory Performance

Allocation of resources: `1` vCPU, `4096`MB of Memory

The following table is the result of stream memory performance test.

| - | Add(GB/s) |  Copy(GB/s) | Scale(GB/s) | Triad(GB/s) |
| --- | --- | --- |--- |--- |
| host | 13.03 | 12.78 | 12.70 | 13.10 |
| docker | 12.98 | 12.67 | 12.62 | 12.87 |
| hyper | 12.80 | 12.56 | 12.66 | 12.81 |


## 6. Testing environment

Bare Metal Server(Type 1) on `packet.net`

| - | Configuration |
| --- | --- |
| Server | E3-1240 v3 @ 3.4 Ghz |
| RAM | 16GB DDR3-1333 RAM |
| OS | Ubuntu 14.04.2 LTS (64 bit) |
| Disk | 2 x 120GB Enterprise SSDs |
| Network | 2 x 1Gbps Bonded Network |

> Detailed configuration: https://www.packet.net/pricing/
