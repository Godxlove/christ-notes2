# system calls
- Programming interface to the services provided by the OS
- Typically written in a high-level language (C or C++)
- Mostly accessed by programs via a high-level Application Programming Interface (API) rather than direct system call use

Three most common APIs are Win32 API for Windows, POSIX API for POSIX-based systems (including virtually all versions of UNIX, Linux, and Mac OS X), and Java API for the Java virtual machine (JVM)

<br>

![](system_call_eg.png)

![](eg_of_standardAPI.png)

---

# system call implementation
- Typically, a number associated with each system call
	- System-call interface maintains a table indexed according to these numbers
- The system call interface invokes  the intended system call in OS kernel and returns status of the system call and any return values
- The caller need know nothing about how the system call is implemented
	- Just needs to obey API and understand what OS will do as a result call
	- Most details of  OS interface hidden from programmer by API 
		- Managed by run-time support library (set of functions built into libraries included with compiler)

---

### diagram
![](system_call_API_pic.png)

---

## system call parameter passing
- Often, more information is required than simply identity of desired system call
	- Exact type and amount of information vary according to OS and call
- Three general methods used to pass parameters to the OS
	- Simplest:  pass the parameters in registers (In some cases, may be more parameters than registers)
	- Parameters stored in a block, or table, in memory, and address of block passed as a parameter in a register. (approach taken by Linux and Solaris)
	- Parameters placed, or pushed, onto the stack by the program and popped off the stack by the operating system
	- Block and stack methods do not limit the number or length of parameters being passed

<br>

![](parameterPassing_viaTable_pic.png)

---

## types of system calls
**Process control**
- create process, terminate process
- end, abort load, execute
- get process attributes, set process attributes
- wait for time
- wait event, signal event
- allocate and free memory
- Dump memory if error
- Debugger for determining bugs, single step execution
- Locks for managing access to shared data between processes

<br>

**File management**
- create file, delete file
- open, close file
- read, write, reposition
- get and set file attributes

<br>

**Device management**
- request device, release device
- read, write, reposition
- get device attributes, set device attributes
- logically attach or detach devices

<br>

**Information maintenance**
- get time or date, set time or date
- get system data, set system data
- get and set process, file, or device attributes

<br>

**Communications**
- create, delete communication connection
- send, receive messages if message passing model to host name or process name
- From client to server
- Shared-memory model create and gain access to memory regions
- transfer status information
- attach and detach remote devices

<br>

**Protection**
- Control access to resources
- Get and set permissions
- Allow and deny user access

<br>

![](windows_linux_sysCalls.png)

