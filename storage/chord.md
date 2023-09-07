# Chord: A Scalable Peer-to-peer Lookup Service for Internet Applications (2001) 
This paper is about a new scalable distributed protocol for lookup in a dynamic p2p system with frequent node arrivals and departures. They achieve this by having a routing table with information of fewer other nodes, and consistent hashing to create identifiers for keys & nodes. 

**Key**: performance, simplicity 

## Key Techniques 
* Identify the core operation in most p2p system: efficient location of data items
    *  Main operation: "given a key, it maps the key onto the node"  
* Consistent hashing: load balancing, involves little movement of keys when nodes join and leave
    *  Idea: hash both the object and the server
    *  Connect both ends of the hash to form a hash ring
    *  To locate the server for a particular object by going clockwise
    *  Pros: adding and removing new server only requires redistribution of a fraction of the keys
*  Implement consistency hashing?
    *  Option 1: every node knows location of every other node - lookup O(1), tables O(N)
    *  Option 2: every node only knows successor - Table O(1), Lookup O(N)   
* Finger table: store only a few information about other nodes in each node for efficient lookup
    *  Every node knows M other nodes in the ring  
    *  Lookup efficiency in $N$ node network: $O(log N)$  
