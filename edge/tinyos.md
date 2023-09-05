# System Architecture Directions for Networked Sensors (2000)
The paper was primarily motivated by the emerging significance of low-power, integrated networked sensors and the unique challenges they present. Traditional OS models were not fit for the constrained resources available on sensor nodes. The key requirements under this type of low power wireless communication environment are
1. _Resource Efficiency_: Sensor nodes are constrained by power, computation, and storage resources
2. _Modularity_: Easy to compose yet sufficiently decoupled components.
3. _Fine-grained concurrency_: Sensors operate in a highly concurrent environment due to the multitasking nature of sensing, processing, and communication.
 

TinyOS is a tiny **event-driven** operating system that provides support for efficient modularity and **concurrency-intensive** operation that fits for this context. 

## Key Ideas 
* Support concurrency
    * Event-driven architecture
* Software modularity
    *  Application = scheduler + graph of components
    *  _Component_: contains commands, event handlers, internal storage, and tasks
    *  _Scheduler_: schedules the components 
*  Efficiency
    *  Get done quickly and then sleep
    *  Static memory allocation
        *  No heap (malloc), no function pointers, no dynamic runtime allocation    

### Component
A component processes commands, throw events, has a frame for storing local state, and use task for concurrency. It also provide interfaces used by other components to communicate with it. 
<img width="472" alt="image" src="https://github.com/lynnliu030/os-prelim/assets/39693493/955848e7-2cd0-4ddf-a0d8-30de0286d149">

## Compared 
* Thread-based model: scheduler activations, cappricio
* Event-based system like TinyOS: SEDA 
