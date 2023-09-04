# The Structuring of Systems Using Upcalls (1985)
The paper introduces the concept of **"upcalls,"** a mechanism allowing lower layers in a system to call back into higher layer (e.g., through runtime-bound handlers). Upcalls are positioned as an alternative to traditional "downcalls" or system calls, which follow the top-down control flow typical in systems.

## Baselines: Layer as Processes
Implement each layer as a process 

- Different address space, so no corruption
- All inter-module communication is async now (i.e. via async inter-process communication (IPC))
- Downcalls: control flow from top to down
    - Application calls a library
    - Library calls the system
    - The lower level executes for a while, then returns to upper level
- Cons: serious performance problem, and natural flow is not always downward 

## Key Techniques 
Some techniques mentioned in the paper: 
1. **Single Address Space**: all modules are kept within a single address space to allow for direct procedure calls between them.
2. **Multi-threading**: modules efficiently use upcalls and downcalls
3. **Flexible Control Flow**: unlike downcalls, which only go from higher-level modules to lower-level ones, upcalls provide a two-way interaction, allowing for more dynamic and adaptive system behavior.

### Examples 
Downcall-based socket 

- Downcall: Create and bind a socket
- Downcall: Receive data if possible
- Downcall: Send data if possible
- Downcall: Tell me when i can send or receive more data on any of these sockets

Upcall-based socket 

- Downcall: create and bind a socket
    - We also need to tell the socket layer which procedures to use as upcalls
- Upcall: some data just arrived
- Upcall: do you have any data to send?
- Downcall: call me back if you can, I have data to send

### Pros
* **Efficiency**: allow sync subroutine calls v.s async IPC, no polling overhead, higher level receives direct notification of changes 
* **Simplicity**: eliminate code for data buffering, low leve can ask upper level for "advice" (i.e. "piggybacking" in network) 
* **Usability**: programmers more familiar with subroutine interface than IPC, some thread design decisions can be delayed

### Cons
* **Upward dependency and fault tolerance**: lower levels are often shared among different upper levels clients, failures may affect higher layers as well, poses challenges in releasing resources and corruption of state
* **Security**: since modules which need to be protected from each other can still sahre an addr space. We need garbage collection and high-level language for safe access to the single address space. 
