# Kwarantine is a light-weight hypervisor Coming soon!

![Kwarantine](https://web.archive.org/web/20210529223532im_/https://kwarantine.xyz/static/img/arch1.png)

We've been working on a new [hypervisor](https://web.archive.org/web/20210529223530/https://kwarantine.xyz/) that can run strongly-isolated workloads (Docker containers or worker functions) on bare metal (i.e., no VMs!) resulting in 1000x more workloads on the same hardware at native performance (i.e., cold start in seconds with no runtime virtualization tax!).

This is still a WIP, but we wanted to give the community an idea about our approach, its benefits, and various use cases it unlocks. Today, VMs are used to host containers, and make up for the lack of strong security as well as kernel isolation in containers. This work adds this missing security piece in containers. 

We plan on launching a free private beta soon. Meanwhile, we'd deeply appreciate any feedback, and happy to answer any questions here or on our [slack channel](https://join.slack.com/t/kwarantine/shared_invite/zt-pzjlch5s-H610hE5y9fenswhPi2MVvg). 

Thanks!

# Comparison

* **Xen** is a full-fledged hypervisor that hosts VMs. It uses QEMU for I/O emulation in VMs, which increases the attack surface.

* **gVisor** intercepts app syscalls and serve them in user space (inside separate VMs, one for each container), which reduces runtime performance significantly. Performance numbers on gVisor are available in Fig 3--11 [here](https://www.usenix.org/system/files/hotcloud19-paper-young.pdf). 

* Although **Firecracker** improved bootup time, it also uses VMs to sandbox container code. However, VMs incur high runtime overhead (not to be confused with fast booting) and need to be provisioned. Performance numbers on Firecracker are available in Fig 8/9 [here](https://www.usenix.org/system/files/nsdi20-paper-agache.pdf).

* **Kwarantine** is a thin hypervisor that directly runs containers/workers on the hardware (no VMs). It uses hardware virtualization extensions, MMU, and page tables to provide the same level of security as VMs. Each container runs with a separate copy of the host kernel so that vulnerabilities/bugs are isolated. It does not use QEMU. We will post detailed technical docs on design/features and performance evaluation soon.

# Use caes

* Secure isolation of apps/services w/o the virtualization tax
* Long running serverless workers
* Fast secure execution environment for AI agents.
