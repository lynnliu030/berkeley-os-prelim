# System Structure 
## Flexibility v.s Reliability v.s Security 

### Monolithic Kernel
1. Flexibility: Limited, everything's in one big codebase.
2. Reliability: Generally stable but one bug can crash all.
3. Security: Generally secure but one flaw can be disastrous.
4. When to Use: Ideal for general-purpose desktop operating systems where performance is a priority and the software ecosystem is well-established. Examples include Linux and traditional UNIX systems.
5. Why: They are typically faster and have been heavily optimized over years of development.

### Microkernel
1. Flexibility: High, very modular.
2. Reliability: Stable, isolated modules.
3. Security: Secure but slower due to isolation (i.e. lots of context switches, IPC between components) 
4. When to Use: Critical systems where high security and reliability are essential, like in avionics, automotive safety systems, and medical equipment.
5. Why: The isolated modular components make it easier to verify system correctness and improve security.

### Hybrid Kernel
1. Flexibility: Balanced, best of both monolithic and microkernel.
2. Reliability: Generally stable, depends on implementation.
3. Security: Balanced, but complexity can introduce flaws.
4. When to Use: General-purpose systems where a balance of performance, security, and reliability is needed. Microsoft's Windows NT is a good example.
5. Why: They aim to combine the best features of both monolithic and microkernels, making them versatile for a variety of applications.
   
### Exokernel
1. Flexibility: Very high, direct hardware access.
2. Reliability: Risky, bad code can crash system.
3. Security: Less secure, minimal isolation.
4. When to Use: Highly specialized applications or systems that require maximum hardware performance and minimal overhead, like High-Performance Computing (HPC) or real-time systems.
5. Why: They allow applications to communicate directly with the hardware, ensuring minimal overhead.

### Multi-kernel 
1. Flexibility: Adaptable across multiple CPUs/cores.
2. Reliability: Redundancy can improve stability.
3. Security: Varies, but distribution can help.
4. When to Use: Systems that need to scale across multiple heterogenous cores, CPUs, or even separate machines efficiently, such as cloud computing environments and data centers.
5. Why: Designed to distribute tasks horizontally, they can offer high performance in distributed computing environments.

## Design Tradeoffs 
* Import functionality into kernel vs expose hardware?
* Cost of abstrations
* Monolithic kernels v.s microkernels 
