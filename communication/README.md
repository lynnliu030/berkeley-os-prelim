# Communication 
Reference: https://github.com/parasj/papers/tree/master/communications

When we think about communication, we need to think about multiple layers. 

1. Local communication: IPC related concepts, shared memory v.s message passing
2. Remote communication: how to build a reliable transport? (i.e. UDP v.s TCP) What abstractions of communication should we use when building a distributed system? How to make it efficient and fast? How to make it secure? 

Upcall and LRPC focus on local communication (different aspects, vertically and horizontally), and active messages focus on remote communication. These three papers are all primarily concerned with performance. 
 
 ## RPC: an abstraction for communication  
Just a PL abstraction, create wrappers so calling a function on another machine just feels like calling a local function. The stub function removes the pain of packing function arguments and results into messages by automating it. This also systems to communicate across multiple languages. Protobuf is an example of a serialization/deserialization format across languages.

LRPC deals with making RPC lightweight. Active Messages offers an alternative model where message handlers are triggered to initiate computation. 

## RPC: need low latency 
Low latency is critical for good RPC performance. Active Messages demonstrate attention paid to optimize latency for small messages. These needs sometimes bypass the conventional networking stack. 

## Computation and communication overlap 
Active Messages strived to interleave execution with communication. This disguises the latency of the network. In order to enable the processor to remain utilized, interleaving is important.

## Security v.s Performance 
Many RPC libraries make security tradeoffs to improve performance. For example, LRPC is where clients execute code directly in the server's domain. For upcalls, single address space makes things faster but also there is a risk on isolation and upward dependencies. 
