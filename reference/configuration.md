# Configuration

## Configuration file

The configuration file of Hyper is located under `/etc/hyper.conf`. The file is in INI format：

    Host   = tcp://localhost:1246
    Bios   = /var/lib/hyper/bios.bin
    Cbfs   = /var/lib/hyper/cbfs.rom
    Kernel = /var/lib/hyper/kernerl-4.0.1
    Initrd = /var/lib/hyper/initrd.img
    Bridge = hyper0
    BridgeIP = 192.168.123.1/24

#### Parameters

- `Host`: bind hyperd's socket to the IP and Port, by default hyperd listens on `unix:///var/run/hyper.sock`
- `Bios`: the BIOS binary file path, by default `/var/lib/hyper/bios.bin`
- `Cbfs`: the CBFS ROM file path, by default `/var/lib/hyper/cbfs.rom`
- `Kernel`: the path of the HyperKernel, by default `/var/lib/hyper/kernel-4.0.1`
- `Initrd`: the path of the initrd file, by default `/var/lib/hyper/initrd.img`
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

