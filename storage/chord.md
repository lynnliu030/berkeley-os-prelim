# Chord: A Scalable Peer-to-peer Lookup Service for Internet Applications (2001) 
This paper is about a new scalable distributed protocol for lookup in a dynamic p2p system with frequent node arrivals and departures. They achieve this by having a routing table with information of fewer other nodes, and consistent hashing to create identifiers for keys & nodes. 

## Key Techniques 
* Identify the core operation in most p2p system: efficient location of data items
* Consistent hashing: load balancing, involves little movement of keys when nodes join and leave
* Finger table: store only a few information about other nodes in each node for efficient lookup
    *  Lookup efficiency in $N$ node network: $O(log N)$  
