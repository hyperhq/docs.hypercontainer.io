# Performance

>The following test was executed on [`Packet`](http://www.packet.net) Bare Metal Server  
 - `Type 1` : 8vCPU(3.4 Ghz) + 16GB(DDR3) + SSDs(2x120GB)  
 - `Type 3` : 32vCPU(2.6 Ghz) + 128GB(DDR4) + SSDs(2x120GB) + NVMe(2x800GB)

>To see [test result](perf-on-softlayer.md) on IBM SoftLayer Bare Metal Server

## 1. Time

### 1.1 Pod startup time

Run a new Pod only takes `376` millisecond (ms) on `Type 1`

| - | with-qboot | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- | --- |
| Hyper for KVM | Yes | 352 | 391 | 376 |
| Hyper for KVM | No | 685 | 725 | 709 |
| Hyper for QEMU | Yes | 1348 | 1380 | 1367 |
| Hyper for QEMU | No | 1773 | 1809 | 1787 |
| Hyper for XEN | No | 2426 | 2486 | 2449 |


Run a new Pod takes `519` millisecond (ms) on `Type 3`

| - | with-qboot | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- | --- |
| Hyper for KVM | Yes | 469 | 571 | 519 |
| Hyper for KVM | No | 821 | 961 | 915 |
| Hyper for QEMU | Yes | 1773 | 2006 | 1862 |
| Hyper for QEMU | No | 2188 | 2459 | 2296 |
| Hyper for XEN | No | 3171 | 3345 | 3269 |

>The following tests are for "Hyper for KVM" with qboot

### 1.2 Pod replace time

Replace a running Pod with a new one, only takes `150` ms on `Type 1`

| -   | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- |
| replace time | 128 | 171 | 150 |


Replace a running Pod with a new one, takes `174` ms on `Type 3`

| -   | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- |
| replace time | 163 | 184 | 174 |



## 2. Density Test

In the same condition, Hyper can run more Pods than traditional VMs, and there is more available memory for user's applications.

**Test method:**  Create VM/pod ceaselessly, until "Cannot allocate memory" occurs or reach maximum of tap device.

  - Allocation of resources : `1` vCPU, `512`MB Memory
  - Test Docker image  
  	ubuntu:14.04 - https://registry.hub.docker.com/_/ubuntu/
  - Test KVM image
  	http://cloud-images.ubuntu.com/releases/14.04/release-20150706/ubuntu-14.04-server-cloudimg-amd64-disk1.img


#### 2.1 Test result on `Type 1`

1) Max traditional VM(KVM) number : `105`

> **QEMU process memory usage**(MB): (105 QEMU processes)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    70 |   184 |   `156` |
|VSZ(VmSize)|   928 |   928 |   928 |

> **memory usage in VM** (MB): (105 running VMs)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   490 |   490 |   490 |
|Used |    123 |    124 |    `124` |
|Free |   366 |   367 |   `366` |


2) Max Pod(Hyper) number: `252`

> **QEMU process memory usage**(MB): (252 QEMU processes)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    61 |    75 |    `69` |
|VSZ(VmSize)|   994 |  1066 |   995 |

> **memory usage in Pod**(MB): (252 running Hyper Pods)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   498 |   498 |   498 |
|Used |    14 |    14 |    `14` |
|Free |   484 |   484 |   `484` |


#### 2.2 Test result on `Type 3`

1) Max traditional VM(KVM) number : `627`

> **QEMU process memory usage**(MB): ( 627 QEMU process )

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    62 |   232 |   211 |
|VSZ(VmSize)|   928 |   928 |   928 |

> **memory usage in VM** (MB): (627 running VMs)

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   490 |  490 |   490  |
|Used |   242 |  243 |  `243` |
|Free |   246 |  247 |  `247` |



2) Max Pod(Hyper) number on `Type 3` : `1023`

> **QEMU process memory usage**(MB): ( 1023 QEMU process )

|  -  | min | max | avg |
| --- | --- | --- | --- |
|RSS(VmRSS) |    69 |    75 |    72 |
|VSZ(VmSize)|   994 |  1066 |   994 |


> **memory usage in container**(MB): ( 1023 running Hyper Pods )

|  -  | min | max | avg |
| --- | --- | --- | --- |
|Total|   498 |   498 |   498 |
|Used |    14 |    14 |    `14` |
|Free |   484 |   484 |   `484` |




## 3. Memory Utilization

### 3.1 Minimum startup memory

The minimum startup memory is `28`(MB)


### 3.2 QEMU process memory usage

When starting a Pod with minimum startup memory, QEMU process uses `50`MB of the Host OS' physical memory.

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

| Target | DMIPS(Type 1) | DMIPS(Type 3) |
| --- | --- | --- |
| Host | 24938 | 21457 |
| Docker | 24875 | 21444 |
| Hyper | 24817 | 20500 |

> In the Target column,  `Host` means Host OS, `Docker` means Docker container, `Hyper` means Hyper Pod


The following table is the result of `whetstone` CPU performance test.

| Target | MFLOPS(Type 1) | MFLOPS(Type 3) |
| --- | --- | --- |
| Host | 5064 | 4522 |
| Docker | 5056 | 4516 |
| Hyper | 5050 | 4503 |


## 5. Memory Performance

Allocation of resources: `1` vCPU, `4096`MB of Memory

The following table is the result of stream memory performance test on `Type 1`

| Target | Add(GB/s) |  Copy(GB/s) | Scale(GB/s) | Triad(GB/s) |
| --- | --- | --- |--- |--- |
| Host | 13.10 | 12.78 | 12.70 | 13.03 |
| Docker | 12.98 | 12.67 | 12.62 | 12.87 |
| Hyper | 12.91 | 12.56 | 12.66 | 12.80 |

The following table is the result of stream memory performance test on `Type 3`

| Target | Add(GB/s) |  Copy(GB/s) | Scale(GB/s) | Triad(GB/s) |
| --- | --- | --- |--- |--- |
| Host | 15.17 | 13.71 | 13.79 | 15.00 |
| Docker | 15.13 | 13.77 | 13.72 | 14.94 |
| Hyper | 14.20 | 12.83 | 12.88 | 14.14 |


## 6. Testing environment

** Bare Metal Server configuration**

| - | Type 1 | Type 3 |
| --- | --- | --- |
| Server | E3-1240 v3 @ 3.4 Ghz | 2 x E5-2640 v3 @ 2.6 Ghz |
| RAM | 16GB DDR3-1333 RAM | 128GB DDR4-2100 RAM |
| OS | Ubuntu 14.04.2 LTS (64 bit) | Ubuntu 14.04.2 LTS (64 bit) |
| Disk | 2 x 120GB Enterprise SSDs | 2 x 120GB Enterprise SSDs + 2 x 800GB NVMe Flash Drives |
| Network | 2 x 1Gbps Bonded Network | 2 x 10GBit SFP+ Bonded Network |

> Detailed configuration: https://www.packet.net/pricing/
