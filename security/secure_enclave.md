# Secure enclave and edge computing 

Reference: 
* https://opaque.co/what-are-secure-enclaves/
* https://www.trentonsystems.com/blog/what-is-intel-sgx
  
## Motivation: secure environment for data processing  
We want to eliminate the need to trust Infrastructure as a Service (IaaS) providers by creating a provably secure environment for data processing. This is critical in multi-tenant, cloud, or edge computing environments where data breaches and insider threats are a concern.

## Secure Enclave 
_definition_: a computing environment that isolates code and data from the OS and privileged users. 

-  Even users with root access to the machines and OS should not be able to learn the contents of secure enclave memory or tamper with the execution of code inside the enclave.
-  All of the major cloud providers now have secure enclave offerings. 

### Comparisons with traditional encryption 
* Data-at-rest: stationary data stored in non-volatile memory such as cloud storage or hard drives
* Data-in-motion: data actively being transmitted, typically over some network
* Data-in-use: data actively processed by a system for some application. Various secrets such as keys and passwords are some candidates that need to be secured
  
Most systems today protect _data-at-rest_ and _data-in-motion_ using **SSL/TLS, symmetric, and asymmetric key encryption**. When data needs to be used, its contents are decrypted in memory. 

Problem of _**data-in-use**_: an application that operates on some data must be able to see the data, but if data is sensitive, user must trust the application is not leaking data and platform that application runs is secure. 

Current approach such as access control is susceptible to human error and does not protect against informaiton leakage; homomorphic encryption (HE) allows computations directly performed on encrypted data, but is too slow. 

## Intel's SGX 
Intel's Software Guard Extensions (SGX) offers **hardware-based** memory encryption that isolates specific application code and data in memory.

<img width="846" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/0032f272-4989-426d-a9bb-d5881afd2164">

>At runtime, Intel SGX instructions build and execute the enclave into **a special encrypted memory region** with **restricted entry/exit location** defined by the developer. This helps prevent data leakage. Enclave code and data inside the CPU perimeter runs in the clear, and enclave data written to memory is encrypted and its integrity checked, helping provide some assurance that no unauthorized access or memory snooping of the enclave occurs.

## Usecases 
With a secure enclave environment, parties can finally efficiently collaborate by contributing individual data for some larger computation without other parties or any third parties ever learning any private data. 

This is suitable for 
* Runtime applications, protected through execution with SGX
* Securing IoT edge device communication between cloud and client
* Collaborative computing, financial services, healthcare, manufacturing, etc. 

E.x. Communication between senders and receivers: Imagine a secure messaging application where even the service provider should not have access to the messages. SGX enclaves could be used to encrypt messages on the sender's side and decrypt them on the recipient's side, ensuring end-to-end confidentiality and integrity.

E.x. IoT edge communication: In IoT applications, the edge devices often collect sensitive information that is sent to a central server for processing. SGX can be used to encrypt this data securely at the source, ensuring that any interception at any point between the edge device and central server will not compromise the data. It's also useful for securely updating the software running on IoT devices.

E.x. cloud processing sensitive information: A cloud computing service that processes confidential medical images could take advantage of SGX by having users upload encrypted images, with the encryption keys being sent by the users to the software running within a secure enclave. This enclave contains the processing algorithm and the protected code for encrypting and decrypting the images. The code that receives the uploaded encrypted images and stores them would be left outside the enclave.

Example steps
1. _Initial Communication_: User communicates with the cloud service via SSL/TLS to establish a secure channel.
2. _Remote Attestation_: Intel SGX enclave on the cloud server can provide a proof of its legitimacy through remote attestation. This ensures the user that they are communicating with a genuine, secure enclave.
3. _Encrypting the Images_: User uses a symmetric (asymmetric) encryption algorithm to encrypt the sensitive medical images. 
4. _Transmitting the Encrypted Images and Key_: The encrypted images and encryption key are sent to the cloud server over secure channel.
5. _Enclave Processing_: The enclave decrypts and subsequently processes the images, maintaining the confidentiality and integrity of the sensitive data.
6. _Storing Encrypted Images_: storing and receiving encrypted data outside enclave does not expose sensitive information
