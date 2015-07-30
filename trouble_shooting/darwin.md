# FAQ on Mac/VirtualBox Support

> VirtualBox is an open source hypervisor by Oracle.

## How to get verbose messages

For Mac users, the log is located at `/var/log/hyper/`, and if you met any unknown problems, you can get more detail debug info with the following steps ---

- Stop hyperd service:

      sudo launchctl unload /Library/LaunchDaemons/sh.hyper.hyper.plist

- Edit the service configuration `/Library/LaunchDaemons/sh.hyper.hyper.plist`, this is the default configuration:

        <?xml version="1.0" encoding="UTF-8"?>
		<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
		<plist version="1.0">
		<dict>
		  <key>Label</key>
		  <string>sh.hyper.hyper</string>
		  <key>ProgramArguments</key>
		  <array>
				<string>/opt/hyper/bin/hyperd</string>
				<string>--config=/opt/hyper/etc/hyper/config</string>
				<string>-v=1</string>
				<string>--nondaemon</string>
		  </array>
		  <key>EnvironmentVariables</key>
		  <dict>
			  <key>PATH</key>
			  <string>/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin</string>
		  </dict>
		  <key>RunAtLoad</key><true/>
		  <key>KeepAlive</key><true/>
		  <!-- If you met any problems, uncomment this block to enable more output from launchd
		    <key>StandardErrorPath</key>
		    <string>/var/log/hyper/launchd.stderr.log</string>
		  -->
		</dict>
		</plist>

  enable the `StandardErrorPath` will get more output from the daemon, adjust `-v=1` to `-v=4` will open VirtualBox GUI.

- Reload the service

	  sudo launchctl unload /Library/LaunchDaemons/sh.hyper.hyper.plist

  and wait some seconds.

## VirtualBox Problems

#### I met some virtualbox `medium` problem

Check your VirtualBox version. Hyper support the VirtualBox 5.0 released in July 2015. And don't worry, latest vagrant also support VirtualBox 5.0.

#### I cannot find the VMs in VirtualBox

Hyper Daemon is running as `root`, you can use `sudo vboxmanage list vms` to find the VMs created by hyper.

#### What is VM `hyper-mac-pull` VM, is it necessary?

It help to build the image layers downloaded from Hub, and help manages the defferencing images. It configured with 64MB memory. Thanks to that Hyper is run on hypervisor and support hot plug, hyper can use a light weight Hyper VM to manage images in a disk efficiently and cross platform way. 

Due to the restrictions from VirtualBox and Mac, it is the necessary way to balance the disk consumption, compatibility, and memory. 

It will be terminate when daemon is stopped.

#### How to delete a VM outside hyper

Use `vboxmanage list vms` to find it, `vboxmanage controlvm {name or id} poweroff` to turn off it, `vboxmanage unregistervm {name or id} --delete` to delete it at all.

#### Oops, I delete the `hyper-mac-pull`

Stop and start daemon should help, If not, re-install the pkg.

## Image and Volumes Problems

#### Does the Image consumes much? Does Hyper Mac support layered storage?

Yes, we use differencing vdi image by default, it is a bit like devicemapper's copy on write snapshot.

#### I cannot instert volume

There is some restriction because Mac OS X does not support bind mount. We use dir hardlink of HFS+, the restrictions are:

- *The file system must be journaled HFS+* --- Only can map dir in same HFS+ volume with `/var/lib/hyper`, and if you want to change the hyper runtime dir, look at the configuration file at `/opt/hyper/etc/hyper/config`.
- *The parent directories of the source and destination must be different *--- This is not a problem
- *The source’s parent must not be the root directory* --- This is OK for most cases, remeber that `/var` is under `/private` actually.
- *The destination must not be in the root directory* --- This is OK
- *The destination must not be a descendent of the source* --- Don't to map `/var`, `/var/lib`, `/var/lib/hyper`, `/var/lib/hyper/run`. 
- *The destination must not have any ancestor that’s a directory hard link* --- the above directories should not be a HFS+ dir hardlink

And hyper also shipped a tool to unlink the dir hardlink manually: `/opt/hyper/bin/hunlink`.

## Environment cleanup and Uninstall

#### Is it safe to re-install the pkg

Yes, the installer will check environment and will not cause data loss.

#### How can I clean uninstall Hyper?

We don't love to know you want to uninstall hyper, but if you want, you can use the script shipped with hyper:

    /opt/hyper/bin/uninstall-hyper.sh --purge

The `--purge` flag will remove not only the binaries, but also all the downloaded images and containers. The runtime file
of hyper are located at `/var/lib/hyper`, and the uninstaller will skip files unknown to hyper under `/var/lib/hyper/run`
to avoid data loss.

The uninstaller will uninstall itself too.

