# Multiprogramming 
Reference very useful summary 
* https://github.com/parasj/papers/tree/master/multiprogramming
* https://pages.cs.wisc.edu/~sschang/OS-Qual/process/process_and_synchronization.htm
* https://w3.cs.jmu.edu/kirkpams/OpenCSF/Books/csf/html/IPCModels.html

Running processes on multicore, multiprocessor systems require coordination, conflict resolution, etc. How to design such systems? How should OS manage memory and schedule tasks? 

## Fundamental Abstraction 
* Process = set of threads + collection of resources
* Thread = a single execution sequence within a process

## Inter-Process Communication (IPC): message passing v.s shared memory 
IPC is a mechanism that allows processes to communicate with each other and synchronize their actions. Processes can communicate with each other through either shared memory model or message passing model.

### Message passing 
Whenever a piece of data is to be exchanged, the process will invoke the kernel with a request to send information to target process. User-mode process will copy data into buffer, then issue a system call to request the data to be transferred. Once kernel is invoked, it will copy the transferred data first to its own memory. Then target process do similar things. 

**Cons**:
* one data exchange invokes two syscalls, one read, one write
* transferred data copied twice (i.e. kernel memory, receiving process) 

### Shared memory 
Processes initially set up a region of their virtual memory to use for IPC. Then it issues a system call to request that the kernel make the region shared. Other processes would do the same. The processes can read from and write to the region as normal, and there is no explicit syscall required to read new data. 

**Pros**: one-time penalty during set-up phase 

**Cons**: synchronization overhead 

## User threads v.s kernel threads 
The tradeoffs between user and kernel threads are demonstrated as follows. Scheduler Activations has a hybrid approach to enable exchange of information between user and kernel, and the main idea is to coordinate user level and kernel level scheduling through scheduler activations. 

### User threads (many-to-one) 
User threads are managed by user level libraries (e.x. scheduling, sync), can be easily implemented by the users.

**Pros**: 1) Implementation is easier, simple, and quick to create 2) It is also fast and efficient: don't need to make system call, context switch is less. 

**Cons**:
* Functionality: OS blocks entire process if one user-level thread blocks an I/O
* OS has no insights on application needs, might make poor scheduling decisions 

### Kernel threads (one-to-one) 
**Pros**: OS sees and understand threads, sync, blocking, etc. 

**Cons**:
* Performance limitations: must go to OS for all operations
* Lack of portability and flexibility: may have limits on # of threads, etc.
