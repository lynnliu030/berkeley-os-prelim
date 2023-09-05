# Isolation and Resource Management 
Resources are often **shared** among multiple users, applications, or services. The need for isolation arises to ensure that these entities do not interfere with each other, either intentionally or unintentionally, in terms of security, resource utilization, performance, and fault tolerance. 

## Virtualization 
[Virtualization](https://github.com/lynnliu030/os-prelim/blob/main/cluster_computing/virtualization.md) allows multiple guest OSes (and their applications) to share the hardware resources of a single physical server. 

* Virtual resources: each OS thinks that it owns the hardware resources
* Virtual machine: OS + applications + virtual resources
* Virtualization layer: management of physical hardware (e.x. VMM, hypervisor)
    *  emulate the behavior the guest OS expects from the HW  

## Containers 
* Containers are lightweight, encapsulated environments that run applications and their dependencies.
* Unlike virtual machines, containers share the host system’s kernel, rather than needing their own operating system.
* Mechanisms: kernel featurers like namespace and cgroups 
    *  Namespacing: isolates process trees, networking user IDs, and mounts
    *  Cgroups: limit and prioritize CPU, memory, block I/Os, and network resources
*  Used in microservices
*  Pros: low overhead
*  Cons: weaker isolation and security guarantees 

## Virtualization v.s Containers
Instead of virtualizing the underlying hardware, containers virtualize the operating system (typically Linux) so each individual container contains only the application and its libraries and dependencies. The absence of the guest OS is why containers are so lightweight and, thus, fast and portable.

LightVM paper discusses the trade-offs between containers and VMs. 
