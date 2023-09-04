# A Hardware Architecture for Implementing Protection Rings (1972) 

The paper discusses protection of segment-based virtual memory as found in Multics. Read, write, and execute permissions are set based on the access level of the process and recorded in segment descriptor words. Flags corresponding to these permissions are checked by hardware upon each reference. 

* Protection rings are nuanced protection modes beyond user/supervisor
* Ring 0 is most priviledged
* Multics segment descriptors indicate the highest ring that is allowed to read or write the segment
* Rings with less privilege of the system do not have execute permissions 

## Hardware support needed
* If OS is designed for portability (i.e. across different hardware platforms), typically only 2 protection modes are used (i.e. user and supervisor) 
* Fault containment: faults only affect lower rings (ring 3 can only affect ring 4)
* Recent OS have hypervisor mode -1 that allows VMM to control ring 0 hardware access
* Ring register: a hardware register that controls memory regions, IO ports and access to special instructions
* CPU loads protection level (ring) from current code segment registers
