# Performance

>The following test was executed on the IBM SoftLayer Bare Metal Server  
  - `Single Intel Xeon E3-1270 v3` : 8vCPU(3.50 GHz) + 32GB(DDR3) + SSDs(400GB)

>To see [test result](perf-on-packet.md) on `Packet` Bare Metal Server


## 1. Time


### 1.1 Pod startup time

Run a new Pod only takes `336` millisecond(ms).

| - | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- |
| startup time  | 314 | 366 | 336 |

>The following tests are for "Hyper for KVM" with qboot

### 1.2 Pod replace time

Replace a running Pod with a new one, only takes `95` ms.

| -   | min(ms) | max(ms) | avg(ms) |
| --- | --- | --- | --- |
| replace time | 80 | 107 | 95 |



## 2. Memory Utilization

### 2.1 Minimum startup memory

The minimum startup memory is `28`(MB)


### 2.2 QEMU process memory usage

When starting a Pod with minimum startup memory, QEMU process uses `49`MB physical memory in Host OS.

|  -  | min(MB) | max(MB) | avg(MB) |
| --- | --- | --- | --- |
|RSS(VmRSS) |    48 |    50 |    49 |
|VSZ(VmSize)|   437 |   438 |   438 |


### 2.3 Memory usage in Pod

When start a Pod with minimum startup memory, there will be `9`MB free memory in a running Pod. Hyper Kernel only takes `11`MB memory.

|  -  | min(MB) | max(MB) | avg(MB) |
| --- | --- | --- | --- |
|Total|    21 |    21 |    21 |
|Used |    11 |    11 |    11 |
|Free |     9 |    10 |     9 |



## 3. CPU Performance

Allocation of resources: 2 CPU, 2048GB Memory

The following table is the result of sysbench CPU performance test. CPU performances in Hyper are pretty close to Host OS.

| Target| num-threads| cpu-max-prime| total time(sec)| resp min(ms)| resp avg(ms)| resp max(ms)|
| --- | --- |--- |--- |--- |--- |--- |
| Host| 1 | 10000| 9.88 | 0.95 | 0.99 | 1.01 |
| Docker| 1 | 10000| 9.89 | 0.95 | 0.99 | 1.12 |
| Hyper| 1 | 10000| 9.92 | 0.95 | 0.99 | 1.28 |
| Host| 2 | 50000| 45.81 | 8.51 | 9.16 | 9.39 |
| Docker| 2 | 50000| 45.83 | 8.50 | 9.16 | 13.17 |
| Hyper| 2 | 50000| 45.97 | 8.95 | 9.19 | 10.22 |

> In the Target column,  `Host` means Host OS, `Docker` means Docker container, `Hyper` means Hyper Pod

## 4. Memory Performance

Allocation of resources: 2 CPU, 2048GB Memory
Test parameter: 1MB block size, transfer datasize is 100GB.

The following table is the result of sysbench memory performance test.

| Target | num-threads |  rnd-read(MB/sec) | rnd-write(MB/sec) | seq-read(MB/sec) | seq-write(MB/sec) |
| --- | --- | --- |--- |--- |--- |
| Host | 1 | 11497 | 11489 | 11487 | 11513 |
| Docker | 1 | 11494 | 11491 | 11494 | 11505 |
| Hyper | 1 | 11417 | 11439 | 11418 | 11419 |
| Host | 2 |22926 | 22835 | 22694 | 22770 |
| Docker | 2 | 22593 | 22828 | 22629 | 22900 |
| Hyper | 2 | 22608 | 22647 | 22737 | 22741 |



## 5. Testing environment

Bare Metal Server on SoftLayer.


| - | Configuration |
| --- | --- |
| Server | Single Processor Quad Core Xeon 1270 V3 - 3.50GHz - 1 x 8MB cache |
| RAM | 32 GB RAM |
| OS | Ubuntu Linux 14.04 LTS Trusty Tahr (64 bit) |
| Disk | 400 GB SSD |
| Uplink Port Speeds | 100 Mbps Public & Private Network Uplinks |

> Detailed configuration: https://www.softlayer.com/Store/orderHourlyBareMetalInstance/37278/66
