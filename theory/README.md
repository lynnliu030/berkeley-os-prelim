# Distributed System Theory 
## Self-guided Questions 
### Lamport Clocks 
1. What problem does this paper aim to solve in distributed systems?
2. Briefly describe the concept of "happens-before" and its relevance in ordering events in a distributed system.
3. How does the paper address the issue of global time in a distributed system?
4. What is a logical clock and how does it differ from a physical clock?
5. Can you explain the algorithm for maintaining the logical clocks in the system?
6. What are the limitations of the methods presented in the paper?
7. How do logical clocks interact with message passing in the system?
8. In what applications or scenarios would the contributions of this paper be most valuable?
9. How has the field evolved since this paper was published? Are the concepts still relevant today?

### General 
1. Explain different failures type
2. Explain different synchrony type 
3. Explain the roles of primary and backups in the system.

### pBFT 
1. How does Practical Byzantine Fault Tolerance (PBFT) improve upon existing fault tolerance mechanisms?
2. Describe the architecture of the PBFT system.
3. Can you explain the three phases of the PBFT protocol?
4. What are the performance implications of using PBFT?
5. What security measures are in place to prevent malicious behavior?
6. How does PBFT deal with a malicious primary?
7. How scalable is the PBFT algorithm?
8. What applications could benefit from adopting PBFT?
9. How has Byzantine Fault Tolerance evolved since this paper? Are there any new methods that improve upon PBFT?

### Viewstamp Replication 
1. What is viewstamped replication, and how does it differ from other replication methods like Paxos or Raft?
2. Why was there a need to revisit Viewstamped Replication? What updates or modifications are introduced in this paper?
3. What are the key components of the system architecture in Viewstamped Replication?
5. How does Viewstamped Replication handle failures?
6. What are the conditions for safely changing views?
7. Discuss the performance trade-offs in adopting Viewstamped Replication.
8. Are there any security considerations in the paper? If not, what could be potential security risks?
9. How would you compare Viewstamped Replication with PBFT?
10. What are some potential applications or real-world scenarios where Viewstamped Replication could be beneficial?
