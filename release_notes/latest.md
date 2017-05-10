# Version 0.8.1 (2017-05-10)

Bug fix:

- Enable vSock, a communication channel between host and guest.
- Kubernetes CRI compatibility issues.
- Container IO stream issues.
- Fixed the Xen build.

The detail of the issues addressed in 0.8.1 could be found [here][milestone-0.8.1]

# Version 0.8 (2017-03-20)

In this release, several significant updates are introduced, such as **Kubernetes Container Runtime Interface (CRI)** support, **OCI images spec** support:

- Feature: Kubernetes CRI support.
- Feature: OCI Image Spec support (`hyperctl save -o nginx.tar -f oci `).
- Interfaces: better GRPC API support.
- Arch: support ARM64 CPUs with GIC version3, e.g. Cavium ThunderX 64-core CPU.
- Enhancement: move all the Pod level logic to hyperd, and runV only maintains the sandbox and containers.
- Enhancement: simplify the model and state machine -- one Pod is one VM.
- Enhancement: allow add/remove containers to/from a Pod/sandbox.
- Enhancement: do not stop sandbox without an explicit stop command even if the last container is stopped (To be compatible to Kubernetes CRI).

And many other improvements and updates.

[milestone-0.8.1]:https://github.com/hyperhq/hyperd/milestone/4?closed=1
