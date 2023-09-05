# Isolation and Resource Management 
The field of computing systems has seen dramatic advancements in how resources — be it CPU, memory, or storage — are managed, isolated, and utilized. From monolithic systems to distributed clusters, and from full-blown operating systems to lightweight containers, the industry has evolved significantly.

There are various aspects of these technologies, from isolation mechanisms like virtualization and containers to more macro-level strategies for resource allocation and process migration in cluster environments.

## Why isolation? 
Resources are often **shared** among multiple users, applications, or services. The need for isolation arises to ensure that these entities do not interfere with each other, either intentionally or unintentionally, in terms of security, resource utilization, performance, and fault tolerance. 

## Virtualization 
Virtualization allows multiple guest OSes to share the hardware resources of a single physical server, managed by a software layer called _hypervisor_. 
### CPU Virtualization 

1. **Full virtualization**
     *  Techniques: bbinary translation and direct execution
         *  Hypervisor translates kernel code to replace non-virtualizable instructions
         *  User-level code runs directly for better performance
     *  Pros: best isolation and security, excellent compatibility (unmodified guest OS) 
     *  E.x. VMware
2. **Paravirtualization**
     *  Techniques: hypercalls 
         *  Involves modify OS kernel
         *  Replace non-virtualizable instructions with hypercalls that communicate directly with the virtualization layer hypervisor
     *  Pros: lower virtualization overhead
     *  Cons: poor compatibility, requires OS kernel modifications 
3. **Hardware-assisted virtualization**
     *  Allow VMM to run in new root mode below ring 0
         *  Privileged calls are set to automatically trap to hypervisor
     *  Pros: excellent compatibility, but some performance issues
   
<img width="1253" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/6d23e632-1de2-4a13-8804-3b99c048875c">

### Memory Virtualization 
The guest OS continues to control the mapping of virtual addresses to the guest memory physical addresses, but the guest OS cannot have direct access to the actual machine memory. The VMM is responsible for mapping guest physical memory to the actual machine memory, and it uses shadow page tables to accelerate the mappings. 

<img width="440" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/eff659fb-83e3-49b8-9085-520888580438">

### Device and I/O virtualization 
The hypervisor virtualizes the physical hardware and presents each virtual machine with a standardized set of virtual devices. These virtual devices effectively emulate well-known hardware and translate the virtual machine requests to the system hardware. 

<img width="346" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/c025a240-2a47-4c7b-b824-b0f8fa7dc8c4">

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
