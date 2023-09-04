# Scale and Performance in a Distributed File System (AFS) (1988)  
> Probably the earliest clear thinking on how to build distributed file systems. A wonderful combination of the science of measurement and principled engineering.

This paper discusses the implementation issues on scale and performance in Andrew File System (AFS) developed at CMU, and discuss the changes made to the original prototype to address these issues. The file system was motivated primarily by considerations of scale. Large scale affects distributed system in terms of performance and operation cost. 

## Motivation: Scale 
The author identifies some key problems to the original AFS prototype via extensive benchmarking: 
1. Path-traversal costs are too high
    1. *Fetch* / *Store* request: pass entire pathname 
    2. CPU time simply walking down directory paths when there’re too many clients 
2. The client issues too many TestAuth protocol messages
    1. Just like NFS 
3. Excessive context switching overhead and high virtual memory paging demands 
4. Server imbalance
