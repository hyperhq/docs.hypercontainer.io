# How it works

On a physical Linux box:

	[root@gnep ~:]# yum install hyper
	[root@gnep ~:]# docker pull nginx:latest
	[root@gnep ~:]# hyper run nginx:latest

Instead of using LXC, Hyper boots the image with a new VM instance:

	[root@gnep ~:]# docker ps
	[root@gnep ~:]#
	[root@gnep ~:]# virsh list
	xxxxxx

## Internal

Hyper is comprised of several components:

- On the (physical) host:
  - Hyper Daemon
  - Hyper CLI
  - (*) REST APIs

- In the VM instance:
  - HyperKernel - a minimalist kernel built for Hyper
  - Hyper Init - a tiny init service

![](https://trello-attachments.s3.amazonaws.com/552cbb0e30cc49001aaa25fc/872x464/7f1c42bbd4d73b17b7fb3670ef4994bb/upload_2015-04-14_at_3.00.26_pm.png)

