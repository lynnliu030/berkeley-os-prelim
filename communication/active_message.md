# Active Messages: A Mechanism for Integrated Communication and Computation (1992) 
**Key idea**: Include code pointer in messages which avoids buffering latency. Code is run immediately on server, thus avoiding as much queueing as possible. Handlers must be fast. Get communication onto network ASAP and off the network into computation ASAP.


The paper discussed how to improve network and computation utilization by modeling the network as a pipeline. Messagers include a pointer to code that is shared on all machines. Messages are sent ASAP with minimal buffering and servers execute code as soon as they recieve a message. This asynchonously frees up the client to continue computing without the overhead of buffering along the network stack.

## Key techniques: active messages
User-Level Handler: Each active message contains the address of a "handler," a small piece of code that resides in the user space.

Message Body: The message body contains arguments or data that the handler will need to execute its operations.

## Workflows 
1. Message Sending: When a processor wants to send data to another, it wraps the data and the handler's address into an Active Message and sends it to the receiving processor.

2. Asynchronous Operation: The sending of the message is asynchronous, meaning the sender does not wait for an acknowledgment from the receiver and continues its own computation.

3. Message Receiving: On the receiving end, the processor reads the Active Message. Rather than buffering the data for later use, it immediately executes the handler specified in the Active Message, passing in the provided arguments.

4. Handler Execution: The handler, being a lightweight piece of code, carries out its operation quickly and integrates the received data into the ongoing computation at the receiver's end. The idea is to get the data "out of the network and into computation" as quickly as possible.
