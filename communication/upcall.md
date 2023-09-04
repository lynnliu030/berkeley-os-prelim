# The Structuring of Systems Using Upcalls (1985)
The paper introduces the concept of **"upcalls,"** a mechanism allowing lower layers in a system to call back into higher layer (e.g., through runtime-bound handlers). Upcalls are positioned as an alternative to traditional "downcalls" or system calls, which follow the top-down control flow typical in systems.

## Baselines: Layer as Processes
- Each layer as a process: different address space, so no corruption
- Serious performance issue! (i.e. polling overhead, data buffering)
- Downcall-based socket 
    - Downcall: Create and bind a socket
    - Downcall: Receive data if possible
    - Downcall: Send data if possible
    - Downcall (polling or callbacks): Tell me when to send / receive more data on any of these sockets

## Key Techniques 
Some techniques mentioned in the paper: 
1. **Single Address Space**: all modules are kept within a single address space to allow for direct procedure calls between them.
2. **Multi-threading**: modules efficiently use upcalls and downcalls
3. **Flexible Control Flow**: unlike downcalls, which only go from higher-level modules to lower-level ones, upcalls provide a two-way interaction, allowing for more dynamic and adaptive system behavior.

### Examples 
1. Downcall (create and bind a socket): application tells the kernel to prepare a socket for network communication just like before, and tell the socket layer which procedures to use as upcalls
2. Upcall (for data and events): when packet comes, kernel can simply calls the relevant function directly; similarly when the kernel determines it's a good time to send data, make an upcall to the procedures
3. Downcall (optional, for additional data): the application can make a downcall to notify the kernel that it has more data to send 

### Pros
* **Efficiency**: allow sync subroutine calls v.s async IPC, no polling overhead, higher level receives direct notification of changes 
* **Simplicity**: eliminate code for data buffering, low leve can ask upper level for "advice" (i.e. "piggybacking" in network) 
* **Usability**: programmers more familiar with subroutine interface than IPC, some thread design decisions can be delayed

### Cons
* **Upward dependency and fault tolerance**: lower levels are often shared among different upper levels clients, failures may affect higher layers as well, poses challenges in releasing resources and corruption of state
* **Security**: since modules which need to be protected from each other can still sahre an addr space. We need garbage collection and high-level language for safe access to the single address space. 
