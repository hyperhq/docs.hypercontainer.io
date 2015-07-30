# About Hyper

Hyper is a **Hypervisor-agnostic Docker Engine** that allows you to run Docker images on any hypervisor (KVM, Xen, etc.).

Technically speaking,

    Hyper = Hypervisor + Kernel + Docker Image

By containing applications within separate VM instances and kernel spaces, Hyper is able to offer an excellent **Hardware-enforced Isolation**, which is much needed in multi-tenant environments.

Hyper also promises **Immutable Infrastructure** by eliminating the middle layer of Guest OS, along with the hassle to configure and manage them.

![](https://trello-attachments.s3.amazonaws.com/55545e127c7cbe0ec5b82f2b/1095x362/558bcbf7a1ab7aa4b4753b1232d3886f/IaaS_vs_CaaS.png)

Performance-wise, **Hyper is super light**:

- **Sub-second Boot**: milliseconds to launch a HyperVM instance
- **Slimmed Footprint**: ~28 MB RAM (512MB on AWS EC2)

With Hyper, the future of Container-as-a-Service is just around the corner.

![](https://trello-attachments.s3.amazonaws.com/552ba9ad83b51945d06ef23b/940x238/9e7346bfd21bc756361c70d8397e76f2/upload_2015-04-13_at_7.58.15_pm.png)

