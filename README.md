# About Hyper

Hyper is a tool (a minimalist kernel called ***HyperKernel***) built for running app container with hypervisor.

Put simply, Hyper allows you to run one or multiple app container images (Docker, ACI) on top of hypervisor.

    Hyper = Hypervisor + Kernel + App Container Image

By running independent kernel in each instance, Hyper is free from the isolation concern of container. Hyper also promises **Immutable Infrastructure** by eliminating the Guest OS middle layer and the hassle to configure and manage the OS.

![](https://trello-attachments.s3.amazonaws.com/552cb61fef93933ed62b9135/871x357/1c24746b58ab3aaadd5988216c8c2df1/upload_2015-04-14_at_3.05.23_pm.png)

Performance-wise, **Hyper is super light**:

- **Sub-second Boot**: 0.5 second to launch a Hyper instance
- **Minimal Overhead**: 1-2% CPU overhead
- **Higher Density**: minimal Mem requirement is 10MB for Hyper (512MB on AWS EC2)

We believe that a secure, public, multi-tenant **Cluster-as-a-Service** (CaaS) can be built with Hyper.

![](https://trello-attachments.s3.amazonaws.com/552ba9ad83b51945d06ef23b/940x238/9e7346bfd21bc756361c70d8397e76f2/upload_2015-04-13_at_7.58.15_pm.png)



