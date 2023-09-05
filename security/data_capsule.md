## Statement: security at the edge 
Applications nowadays reply heavily on data from different sources, i.e. cloud-based DBs, edge-based sensors. The **network's edge**, where much of this data originates, consists of a mix of trusted and untrusted hardware, complicating efforts to verify data integrity and security. 

Current solutions either naively trust the edge hardware or use other methods that do not fully solve the problems of security, privacy, latency, and data integrity. The stakes are high: incorrect or malicious data could lead to disasters, including property damage and loss of life.

## Key techniques 
Key Techniques: DataCapsules and the Global Data Plane (GDP)
**DataCapsules**: They act as cryptographic containers that hold and protect data, much like a physical shipping container secures goods. Each DataCapsule has a unique name and is secured with cryptographic methods, allowing the system to validate the data's integrity and origin. DataCapsules can be deployed in various storage systems.

**Global Data Plane (GDP)**: This is a new data-centric "narrow-waist" networking architecture that focuses on information instead of physical locations (IP addresses). It enables data-centric conversations between clients and DataCapsules based solely on their unique names. It also allows partitioning the network into Trust Domains (TDs) to evaluate the trustworthiness of hardware.

**Secure Computing at the Edge**: The framework leverages trusted computing enclaves like Intel SGX to securely process DataCapsules at the edge of the network, balancing the need for speed and security.

**Intelligent Connected Application**s: Applications like Fog Robotics and online system modeling (Data Twins) are studied and optimized to work within this GDP infrastructure, improving their Quality of Service (QoS), performance, security, and privacy.

**Agile Secure Edge Computing**: Combines the mobility of DataCapsules with secure, lightweight virtual machine containers to enable on-demand, secure computations at the edge.
