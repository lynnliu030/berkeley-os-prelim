# Xen and the Art of Virtualization (2003) 
This paper proposes a practical design for paravirtualized virtual machine. The main goal of the design is performance. 

## Motivation: inefficiency of full virtualization 
To support correct virtualization, certain supervisor instructions must be handled by the hypervisor (VMM), but executing this with insufficient privilege fails silently rather than causing a trap. Full virtualization techniques (e.x. VMWare's ESX) dynamically rewrites portion of the guest machine code to insert traps whenever VMM intervention is required. 

This technique is **complex** and has **high performance cost** particularly for update-intensive operations (i.e. trap every update to maintain consistency with virtual tables). Also, sometimes it is desirable for guest OS to see real resources: i.e. real and virtual time, expose real machine addresses to improve performance. 

## Interface 
1. Memory 
   *  guests have read access to PT but must update them through VMM 
   *  can do batching of updates 
2. CPU
   *  guest OS runs at lower ring than host
   *  guests are aware of virtual and real time
   *  replaces nonvirtualizable instructions with hypercalls that communicate directly with the VMM 
3. I/O
   *  access is through sync I/O rings 
