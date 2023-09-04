# Rethink the Sync (2006) 
The paper introduces external synchrony, a new model for file I/O. The model combines the reliability and simplicity of sync I/O with performance levels close to that of async I/O, being only 8% slower. 

The central problem addressed by the paper is the tension between **durability** and **performance** in file I/O. While sync I/O offers strong reliability and data durability guarantees, it comes at a performance cost and blocks the caller until the operation is complete. On the other hand, async I/O offers better performance but falls short on reliability, ordering, durability, and ease of programming.

## Insights 
The key insight is: it is the end-user, not just the application, who needs the guarantee that a file operation has been successfully completed. This forms the basis for the external synchrony model, which aims to provide guarantees directly to the user rather than just via the application.

## Key Techniques 
_Grouping commits_: Multiple file modifications are grouped together and committed as a single transaction, making the commits atomic.

_Output triggered commits_: The system buffers an application's output instead of displaying it immediately. The buffered output is only released and displayed once the corresponding file modifications have been safely committed.

_Tracking causal dependencies_: The system tracks dependencies between file modifications and external outputs, even when applications communicate via IPC.

The new model builds upon a system called Speculator, initially targeted at improving network performance, to track and propagate causal dependencies.

## Limitations
Crash recovery is a problem in this paper, and there are many extra mechanisms to deal with catastrophic media failures and system crashes (via checkpoints and commits). 
