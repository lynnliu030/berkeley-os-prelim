 # Storage Systems 
| Local FS  | Distributed FS |
| ------------- | ------------- |
| [FFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/ffs.md) (1984) | [NFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/nfs.md) (1985) |
| [JFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/crash_consistency_jfs.md) (1990) | [AFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/afs.md) (1988) |
|  [LFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/lfs.md) (1991) | [CODA](https://github.com/lynnliu030/os-prelim/blob/main/storage/coda.md) (1991) | 
|  | [Sprite](https://github.com/lynnliu030/os-prelim/blob/main/cluster_computing/sprite.md) (1991) |
|  | [GFS](https://github.com/lynnliu030/os-prelim/blob/main/storage/gfs.md) (2003)|

* FFS optimizes performance by changing the on-disk FS layouts
* JFS optimizes for crash consistency by using journalling and re-do logging
* LFS optimizes for small-write performance by write buffering
* NFS optimizes distributed FS crash-recovery by deploying a stateless protocol
* AFS optimizes distributed FS performance by using the callback mechanism, putting some states in the server
* CODA optimizes for availability when the client is disconnected, by using server and client replication, and optimisitic replica control for conflict resolution
* GFS is modern distributed file system that optimizes in DC environment where there is large file, append-only workloads and faults are normal. It deploys a centralized scheduling scheme, decouple control and data (use large chunks), uses data replication to improve scalability and fault tolerance.

## Fault handling v.s crash consistency 

## Lots of small files v.s one large file 

## Sequential v.s random reads / writes 

## Optimized workloads for each case 

## Performance v.s persistence tradeoff 
