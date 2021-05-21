## What is an OS?
![[whatIsAnOS.png]]
![[compSysStruct.png]]
![[4componentsOfCompSys.png]]

<br>

An OS can be viewed by 2 POV - user and system.

![[whatOSdoes.png]]
![[whatOSdoes2.png]]


---
## Types of OS

### BATCH OS

a high level programming lang  makes a .obj file since that is understood by the machine.

whenever you execute a program it creates a process for that program with a unique ID. By using this uniq ID the kernel understands this program is running. This process runs in the RAM.


first P1 runs and after its processes/job has been finished, the CPU moves to moves to P2 and then P3.


### problems
when i/o processes take place, then CPU becomes will become idle (wastage of resources)

Plus, P2 and P3 can't do work unless P1 finishes it (no multitasking)

---
# 07-01-2021 
![[textBooks.png]]


# 12-1-21

![[interrupt_timeline.png]]

![[mitali_text.png]]

watch this [Fetch/Execute/Decode cycle](https://www.youtube.com/watch?v=04UGopESS6A&t=5s)

<br>

![[fetch_decode_cycle1.png]]

PC - program control - has the address of the next work
AC - accumulator is a register
CU - control unit - decodes the instructions
ALU - arithmetic work done
MDR - memory data register - temporarily stores the data
CIR - current instruction register

MEMORY (assembly lang)
load - transferring data from memory to register
add
sto (store) - transferring data from register to memory

<br>

control bus - tells whether to read or write to the memory

---

#### 15 Jan 21
![[storage_device_hierarchy.png]]

SSD to magnetic tapes is RAM (non - volatile)
non-volatile -> info is stored even if electricity goes out.

<br>

#### Volatile memory
cache memory - is between the processor and the main memory.
If processor speed > main memory speed, then cache is required.

stores only min amount of data..the data not available in cache is then taken from main memory

<br>

processor ---> cache ---> Mein memory

<br>

#### when to use the Register variable?
normal variables is stored in main memory.

![[register_eg_program.png]]