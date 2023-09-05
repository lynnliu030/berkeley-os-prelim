# Secure enclave and edge computing 

https://people.eecs.berkeley.edu/~kubitron/courses/cs262a-F19/projects/Suggestion_Docs/Fog_Robotics_Public_Research_Proposal.pdf

## Secure Enclave and SGX 
### Motivation 
The motivation for secure enclave is to eliminate the need to trust Infrastructure as a Service (IaaS) providers by creating a provably secure environment for data processing. This is critical in multi-tenant, cloud, or edge computing environments where data breaches and insider threats are a concern.

_Aggregating data from multiple data sources_ for joint analysis such as rich data analytics and machine learning training has also become an increasingly powerful technique, as witnessed by the increased interest in federating learning and collaborative analytics. The recent advances in secure enclave technologies finally enable such collaboration to occur securely and confidentially.

### Secure Enclave 
A secure enclave, also known as a Trusted Execution Environment (TEE), is a computing environment that isolates code and data from the operating system and even privileged users using hardware-based isolation. It aims to secure data-in-use. 

Most current approaches to protecting data-in-use have relied upon implementing access controls and policies, client-side encryption techniques, and data breach detection, but none are able to prevent the threat in its entirety.

### SGX 

### Usecases 

#### V.s. access control 



### SGX 
Intel's Software Guard Extensions (SGX) aims to proivde integrity and confidentiality guarantees to security sensitive computation performed on a computer where all privileged software (kernel, hypervisor, etc.) is potentially malicious. 

