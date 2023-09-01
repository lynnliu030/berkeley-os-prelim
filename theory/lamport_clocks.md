# Time, Clocks, and the Ordering of Events in a Distributed System

## Motivation: Event Ordering 
* Event ordering is crucial for various aspects of system functionalities such as data consistency, debugging, and coordination.
* There is no single, universally-agreed-upon time or clock that all processes can refer to.
* Synchronizing physical clocks cannot solve the problem due to issues like clock drift and network latency. 

## Summary 
Lamport presents the classic paper about how to define ordering of events in system of colleciton of nodes. 

An event is something happening at one node (i.e. sending or receiving messsage, or local execution step). The key idea about this paper is the concept about **"happened-before" relationship**, which gives us a way to compare two events from potentially different processes.

Lamport introduces **logical clock**, which is the way to count number of events that have occurred. The paper offers a simple algorithm for advancing the logical clocks in a way that respects the happened-before relationship.
1. Each node maintains a counter $t$, incremented on local event $e$
2. When the node sends the message, attach current $t$ to messages sent over the network
3. Recipients move its clock forward to timestamp in the message (if greater than the local counter), then increments 
<img width="550" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/1cef77d0-ee2d-4536-b80d-2e45cfc85591">


**Partial ordering** with lamport clock is useful to establish causation of messages. To produce a **total ordering**, Lamport introduces the notion of tie-breaking based on the deterministic ordering of processes. 

## Limitations 
This paper does not present any mechanisms for failure. Also, given Lamport timestamps $L(a)$ and $L(b)$, with $L(a) < L(b)$, we can't tell whether $a \rightarrow b$ or $a || b$. We can tell something, but can't differentiate the event that is concurrent and the event that one happened before the other. If we want to detect which events are concurrent, we need vector clocks.  
