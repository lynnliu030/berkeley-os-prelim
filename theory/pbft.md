# Practical Byzantine Fault Tolerance (1999) 
PBFT is **efficient** replication protocol extended from Viewstamp Replication that allows the group to survice **Byzantine (arbitrary) failures**. By this time, there was a realization that malicious attacks and Byzantine behavior needed to be dealt with.

## Key Motivation 
Traditional replication protocol (e.x. Paxos, Raft, VR) does not survive Byzantine failures, which are more commonly seen back in the time in forms of mailicious attac, software errors, and so on. 

Exsiting BFT algorithms assume synchrony for safety, but this is dangerous since a malicious attacker can delay messages through DoS, and also they are inefficient. 

## Setup 
### System model 
* Byzantine faults: allow replicas to behave arbitrarily (e.x. not reply, reply bad, accept request but discard state)
* Partial synchrony model: message eventually delivered

### Replica Group 
* Up to $f$ replicas are faulty
* Use $3f+1$ replica group
    *  $N$ replicas, tolerate $f$ non-replies
    *  Then get $N - f$ replicas, worst-case contains $f$ Byzantine faulty replicas
    *  $N - f - f$ none-faulty nodes needs to be larger than $f$ faulty nodes to reach agreement
    *  So $N - 2f > f$, we get $N$ is at least $3f+1$
 
### Architecture
* Primary: order client request
    * execute and reply
* Client: monitor primary, do view-change if necessary
* Difference v.s VR
    *  #1: Replicas are Byzantine
    *  #2: Adversary can control the network: remove messages, corrupt them, etc.
*  Approach     
    *  #1: 3-phase protocol to tolerate $f$ byzantine
    *  #2: use cryptography - all msgs signed by senders
        *  goal: ensure secret keys used by honest is not known to adversay

## Protocol: trust group not individuals 

### Normal Operation Protocol 
<img width="748" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/e9c21dae-d32e-42a9-bf0a-226111de8b8c">

<img width="649" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/e5db621c-2e15-48be-9ac4-3bf15445a02c">

Basic idea: Replica can be faulty! (i.e. assign wrong timestamp, etc.)
Solution: add an extra phase _pre-prepare_ to the protocol to check various details of what the primary is doing and refuse to process messages that are not what they should be. 

Drawback: all-to-all communication with $O(n^2)$ 
