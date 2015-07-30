# Get Started on Mac

This page introduces the daily usage of Hyper for Mac. If you meet any problem not described here, see the [trouble shooting page](../trouble_shooting/darwin.md).

Mac OS X has been introduced in [Hyper v0.3](https://docs.hyper.sh/release_notes/v0.3.html)

## Install

To install Hyper on Mac OS X, you need first to install VirtualBox 5.0, then download and Install the [hyper-mac.pkg](http://hyper-install.s3.amazonaws.com/hyper-mac.pkg)

![Hyper for Mac](https://trello-attachments.s3.amazonaws.com/55b62cf71a91815134fb04d1/620x438/1777c86bec3f4ca95ff9ff5eb8552c39/Install_Hyper_2015-07-30_00-50-54.png)

## Command Line

Hyper for Mac supports the following subcommands in current version.

	  attach                 Attach to the tty of a specified container in a pod
	  build                  Build an image from a Dockerfile
	  commit                 Create a new image from a container's changes
	  create                 Create a pod into 'pending' status, but without running it
	  exec                   Run a command in a container of a running pod
	  images                 List images
	  info                   Display system-wide information
	  list                   List all pods or containers
	  login                  Register or log in to a Docker registry server
	  logout                 Log out from a Docker registry server
	  pull                   Pull an image from a Docker registry server
	  push                   Push an image or a repository to a Docker registry server
	  rm                     Remove one or more pods
	  rmi                    Remove one or more images
	  run                    Create a pod, and launch a new pod
	  start                  Launch a 'pending' pod
	  stop                   Stop a running pod, it will become 'pending'

All the commands support `-h` flag for further information. Specially, the run command supports `-p` flag to run a pod, there are example pods under `/opt/hyper/examples/`.

## Stop and Start the Service

Hyper for Mac service is managed with launchd, use the following command to start/stop it

	sudo launchctl unload /Library/LaunchDaemons/sh.hyper.hyper.plist
	sudo launchctl load /Library/LaunchDaemons/sh.hyper.hyper.plist

And use the following command to check the daemon status.

	> sudo launchctl list sh.hyper.hyper
	{
		"LimitLoadToSessionType" = "System";
		"Label" = "sh.hyper.hyper";
		"TimeOut" = 30;
		"OnDemand" = false;
		"LastExitStatus" = 0;
		"PID" = 32396;
		"Program" = "/opt/hyper/bin/hyperd";
		"ProgramArguments" = (
			"/opt/hyper/bin/hyperd";
			"--config=/opt/hyper/etc/hyper/config";
			"-v=1";
			"--nondaemon";
		);
	};

## Update and Re-Install

Hyper for Mac package can be re-installed, re-install won't cause data loss.

## Uninstall

Hyper for Mac package ships an uninstall script at `/opt/hyper/bin/uninstall-hyper.sh`.

- with `--purge` flag, it will delete hyper and all images and containers
- without the flag, it will keep the images and containers.
