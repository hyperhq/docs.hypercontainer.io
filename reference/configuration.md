# Configuration

## Configuration file

The configuration file of Hyper is located under `/etc/hyper.conf`. The file is in INI format：

	Host   = tcp://localhost:1246
    Bios   = /var/lib/hyper/bios.bin
    Cbfs   = /var/lib/hyper/cbfs.rom
    Kernel = /usr/lib64/hyper/kernerl-4.0.1
    Initrd = /usr/lib64/hyper/initrd.img
    Bridge = hyper0
	BridgeIP = 192.168.123.1/24

#### Parameters

- `Host`: the IP:Port
- `Bios`: the BIOS binary file
- `Cbfs`: the CBFS ROM file
- `Kernel`: path of the HyperKernel, by default `/usr/lib64/hyper/kernel-4.0.1`
- `Initrd`: path of the initrd file, by default `/usr/lib64/hyper/initrd.img`
- `Bridge`: bridge name, default `hyper0`
- `BridgeIP`:  IP range of the bridge, default `192.168.123.0/24`

## CLI usage

	Usage:
	  ./hyperd [OPTIONS]

	Application Options:
	  -config=""            configuration for ./hyperd
	  —v=0                  log level for V logs
	  —log_dir              log directory
	  —host                 host address and port for hyperd (such as —host=tcp://127.0.0.1:12345)
	  —logtostderr          log to stderr instead of log file
	  —alsologtostderr      log to stderr as well as log file

	Help Options:
	  -h, —help             Show this help message

