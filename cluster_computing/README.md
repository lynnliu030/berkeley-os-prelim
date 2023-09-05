# Isolation and Resource Management 
Resources are often **shared** among multiple users, applications, or services. The need for isolation arises to ensure that these entities do not interfere with each other, either intentionally or unintentionally, in terms of security, resource utilization, performance, and fault tolerance. 

## Virtualization 
Virtualization allows multiple guest OSes (and their applications) to share the hardware resources of a single physical server. 

* Virtual resources: each OS thinks that it owns the hardware resources
* Virtual machine: OS + applications + virtual resources
* Virtualization layer: management of physical hardware (e.x. VMM, hypervisor)
  
### CPU Virtualization 

1. **Full virtualization**: binary translation and direct execution
     *  Hypervisor translates kernel code to replace non-virtualizable instructions
     *  User-level code runs directly for better performance
     *  Pros: best isolation and security, excellent compatibility (unmodified guest OS) 
2. **Paravirtualization**: hypercalls 
     *  Replace non-virtualizable instructions with hypercalls that directly talks to hypervisor
     *  Pros: lower virtualization overhead
     *  Cons: poor compatibility, requires OS kernel modifications 
3. **Hardware-assisted virtualization**: root mode 
     *  Allow VMM to run in new root mode below ring 0
         *  Privileged calls are set to automatically trap to hypervisor
     *  Pros: excellent compatibility
     *  Cons: some performance issues
   
<img width="1253" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/6d23e632-1de2-4a13-8804-3b99c048875c">

### Memory Virtualization 
The guest OS controls mapping of virtual addresses to the guest memory physical addresses, but the guest OS cannot have direct access to the actual machine memory. The VMM is responsible for mapping guest physical memory to the actual machine memory, and it uses shadow page tables to accelerate the mappings. 

<img width="440" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/eff659fb-83e3-49b8-9085-520888580438">

### Device and I/O virtualization 
The hypervisor virtualizes the physical hardware and presents each virtual machine with a standardized set of virtual devices (i.e. emulate hardware and translate the virtual machine requests to the system hardware). 

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
