# Kerberos: An Authentication Service for Open Network Systems (1998) 
Kerberos is an authentication network protocol developed by MIT to provide robust and secure authentication system in an open network where users at workstations wish to access services on network servers. Open networks are susceptible to various kinds of attacks, such as eavesdropping, replay attacks, and impersonation. 

The protocol is based on generating tickets 🎫.

## Key Techniques 
There are three components in Kerberos transactions: 
* **KDC (key distribution center)**
  *  Store a copy of all keys (i.e. client keys, service key, and TGS keys) for encryption and decryption purposes
  *  **Authentication server (AS)**: verifying users and authenticating them to the network
  *  **Ticket granting server (TGS)**: responsible for issuing tickets to requested services    
* **Client**: a user requesting access
* **Service**: is what the client requesting access to
  *   E.x. file share servers, DBs, printers, web servers, etc.
 
## Protocol 
In the Kerberos authentication protocol, a user first authenticates with the authentication server to obtain a Ticket Granting Ticket (TGT). When the user needs to access a network service, they use this TGT to request a service-specific ticket from the Ticket Granting Service (TGS), also part of the KDC. This system minimizes the number of times a user needs to enter their password for secure service access. Each step involves encrypted messages and unique session keys to ensure secure communication and prevent unauthorized access.


1. The user sends ticket request <user ID, service ID, TS> access to a service to the authenticator server in KDC.
2. Authenticator server checks the request, create two message to send back
  -  M1
      -  encrypted with client secret key  
      -  <TGS ID, TS, TGS session key>
  -  M2 Ticket Granting Ticket
      -  encrypted with TGS secret key  
      -  <user ID, TGS id, TS, user IP address, lifetime for TGT, TGS session key>
3. The user can now decrypt M1 with their password, get TGS session key, then they send the following messages to TGS
  -  M2: TGT 
  -  M3: <service ID, request lifetime>
  -  M4: User Authenticator <user ID, TS> 
      -  Encrypted by TGS session key
4. TGS receive
  -  verify service ID, if found, grab service secret key
  -  decrypt TGT with TGS secret key, get TGS session key
  -  use TGS session key to decrypt M4
  -  now get TGT and M4, check user ID, TS, and IP addr, also check if M4 in cache or not (replay protection) 
5. TGS send to user 
  -  M5: <service ID, TS, lifetime, Service Session Key>
    -  encrypted by TGS session key
  -  M6: Service Ticket
      -  <user ID, service ID, TS, Service Session Key>
      -  encrypted by Service Secret Key 
6. User
  -  decrypt M5 with TGS session key and get service session key 
  -  send to service
      -  M6: Service Ticket 
      -  M7: User Authenticator <user ID> encrypted with service session key
7. Service
  - Decrypt M6 with service secret key, get service session key
  - Decrypt M7
  - Do similar checking on cache and match
  - Then send back M8: Service Authenticator <Service ID, TS> encrypted by service session key
  - Users can now decrypt with the same symmetric key, verify the service name matches as expected, look at the cache, etc.

## Basics 
1. Mutual Trust via Third Party: The AS and TGS act as trusted third parties. The mutual trust between a user and a service is established indirectly via trust in these servers.

2. Scalability: Because users don't interact directly with service servers for authentication (but go through TGS instead), the system is more scalable. Each service doesn’t need to implement its authentication logic; it just needs to be able to decrypt a message from the TGS.

## Simplified descriptions 
Key Components:
KDC (Key Distribution Center): A trusted server that handles authentication.

Authentication Server (AS): Confirms who users are.
Ticket Granting Server (TGS): Gives tickets for accessing services.
Client: A user who wants to access a service.

Service: What the client wants to use, like a database or a file server.

Simplified Protocol Steps:
Initial Authentication:

Client sends a login request to AS in the KDC.
AS checks the client's identity and sends back two encrypted messages (M1 and M2).
Request for Service Ticket:

Client uses their password to decrypt M1, gets a special key (TGS session key).
Client then sends a new request to TGS with M2 (Ticket Granting Ticket), the desired service's ID, and another message (M4).
TGS validates the request and sends back two new encrypted messages (M5 and M6).
Accessing the Service:

Client decrypts M5 to get another special key (Service Session Key).
Client sends M6 (the Service Ticket) and a new message (M7) to the service.
Service decrypts M6 and M7 and, if everything checks out, allows access.
Verification:

Service sends a final message (M8) back to the client to confirm successful authentication.
Why It Works:
Mutual Trust via Third Party: The client and the services both trust the KDC (AS & TGS). They never need to trust each other directly.

Scalability: Since all services rely on TGS for authentication, it's easier to scale. New services can easily be added without having to design a new authentication scheme for each.

Security: Each step involves encryption and time-stamping, making it tough for unauthorized users to gain access or replay old messages.

Diagram:
Client ----> AS: Initial request
AS ----> Client: M1 and M2
Client ----> TGS: M2, M3, and M4
TGS ----> Client: M5 and M6
Client ----> Service: M6 and M7
Service ----> Client: M8
