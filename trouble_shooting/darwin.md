# FAQ on Mac/VirtualBox Support

> VirtualBox is an open source hypervisor by Oracle.

## How to get verbose messages

For Mac users, the log is located under `/var/log/hyper/`. If you meet any unknown problems, you can get more detailed debug infos with the following steps ---

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

  and wait a few seconds.

## VirtualBox Problems

#### I met some virtualbox `medium` problems

Check your VirtualBox version. Hyper supports the VirtualBox 5.0, released in July 2015. Don't worry, latest vagrant version also supports VirtualBox 5.0.

#### I cannot find the VMs in VirtualBox

Hyper Daemon is running as `root`, you can use `sudo vboxmanage list vms` to find the VMs created by Hyper.

#### What is VM `hyper-mac-pull` VM, is it necessary?

It helps to build the image layers downloaded from Hubs, and helps to manage the defferencing images. It is configured with 64MB memory. Thanks to the fact Hyper is run on hypervisor and supports hot-plug, hyper can use a light weight Hyper VM to manage images in a disk-efficiently and cross-platform way.

Due to the restrictions from VirtualBox and Mac OS X, it is the necessary way to balance the disk consumption, compatibility, and memory.

It will be terminated when the daemon is stopped.

#### How to delete a VM outside hyper

Use `vboxmanage list vms` to find it, `vboxmanage controlvm {name or id} poweroff` to turn it off, `vboxmanage unregistervm {name or id} --delete` to delete it all.

#### Oops, I delete the `hyper-mac-pull`, what can I do?

Stop and start the daemon should help, If not, re-install the pkg.

## Images and Volumes Problems

#### Does the Image consumes much? Does Hyper Mac supports layered storage?

Yes, we use differencing VDI image by default, it is somehow like devicemapper's copy on write snapshot.

#### I cannot insert a volume

There is some restriction because Mac OS X does not support bind mount. We use dir hardlink of HFS+, the restrictions are:

- *The file system must be journaled HFS+* --- Only can map dir in same HFS+ volume with `/var/lib/hyper`, and if you want to change the hyper runtime dir, look at the configuration file at `/opt/hyper/etc/hyper/config`.
- *The parent directories of the source and destination must be different *--- This is not a problem
- *The source’s parent must not be the root directory* --- This is OK for most cases, remeber that `/var` is actually under `/private`.
- *The destination must not be in the root directory* --- This is OK
- *The destination must not be a descendent of the source* --- Don't map `/var`, `/var/lib`, `/var/lib/hyper`, `/var/lib/hyper/run`.
- *The destination must not have any ancestor that is a directory hard link* --- the above directories should not be a HFS+ dir hardlink

Hyper also shipped a tool to unlink the dir hardlink manually: `/opt/hyper/bin/hunlink`.

## Environment cleanup and Uninstall

#### Is it safe to re-install the pkg

Yes, the installer will check the environment and will not cause data loss.

#### How can I clean uninstall Hyper?

We don't love to know you want to uninstall Hyper, but if you want to, you can use the following script shipped with Hyper:

    /opt/hyper/bin/uninstall-hyper.sh --purge

The `--purge` flag will remove not only the binaries, but also all the downloaded images and containers. The runtime file of hyper are located under `/var/lib/hyper`, and the uninstaller will skip files unknown to hyper under `/var/lib/hyper/run` to avoid data loss.

The uninstaller will uninstall itself too.

