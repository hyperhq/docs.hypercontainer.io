# Configuration

The configuration file of Hyper is located at `/etc/hyper.conf`. The file is in INI format：

    [Global]
    Kernel = /usr/lib64/hyper/kernerl-4.0.1
    Initrd = /usr/lib64/hyper/initrd.img
    Bridge = hyper0
    BridgeIP = 192.168.123.1/24

---------------------------------------

### Parameters

- `Kernel`: path of HyperKernel, by default `/usr/lib64/hyper/kernel-4.0.1`
- `Initrd`: path of initrd file, by default `/usr/lib64/hyper/initrd.img`
- `Bridge`: bridge name, default `hyper0`
- `BridgeIP`:  IP range of the bridge, default `192.168.123.0/24`


