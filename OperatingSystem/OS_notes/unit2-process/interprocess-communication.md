# Interprocess Communication
There are two fundamental models of interprocess communication: shared memory and **message passing**.

Shared-memory model -> a region of memory that is shared by cooperating processes is established. Processes can then exchange information by reading and writing data to the shared region.

Message-passing model, communication takes place by means of messages exchanged between the cooperating processes.

![](communication_models.png)

tags - #interprocess #communication

<br>

## Shared-Memory Systems
- requires communicating processes to establish a region of shared memory.
- An area of memory is shared among the processes that wish to communicate. The communication is under the control of the users processes not the operating system.
- Typically, a shared-memory region resides in the address space of the process creating the shared-memory segment.
- Other processes that wish to communicate using this shared-memory segment must attach it to their address space.
- They can then exchange information by reading and writing data in the shared areas.


(more to add - consumer, producer problem with buffer problem)

----

## Message Passing
- Message passing provides a mechanism to allow processes to communicate and to synchronize their actions without sharing the same address space.
- It is particularly useful in a distributed environment, where the communicating processes may reside on different computers connected by a network.

For example, an Internet chat program could be designed so that chat participants communicate with one another by exchanging messages.

Message-passing facility provides two operations:
- send(message)
- receive(message)
 
The message size is either fixed or variable.

---

### Message Passing Types
Logical:
• Direct or indirect
• Synchronous or asynchronous
• Automatic or explicit buffering

---

### Direct Communication
Processes must name each other explicitly:
- send (P, message) – send a message to process P
- receive(Q, message) – receive a message from process Q

Properties of communication link
- Links are established automatically
- A link is associated with exactly one pair of communicating processes
- Between each pair there exists exactly one link
- The link may be unidirectional, but is usually bi-directional

<br>

### Indirect Communication
Messages are directed and received from mailboxes (also referred to as ports)
- Each mailbox has a unique id
- Processes can communicate only if they share a mailbox

**Properties of communication link**
- Link established only if processes share a common mailbox
- A link may be associated with many processes
- Each pair of processes may share several communication links
- Link may be unidirectional or bi-directional

**Operations**
- create a new mailbox (port)
- send and receive messages through mailbox
- destroy a mailbox

Primitives are defined as:
- send(A, message) – send a message to mailbox A
- receive(A, message) – receive a message from mailbox A

<br>

#### Mailbox sharing
- P1, P2, and P3 share mailbox A
- P1, sends; P2 and P3 receive
Who gets the message?

**Solutions**
- Allow a link to be associated with at most two processes
- Allow only one process at a time to execute a receive operation
- Allow the system to select arbitrarily the receiver. Sender is notified who the receiver was.

---

#### Synchronization
Message passing may be either blocking or non-blocking

Blocking is considered synchronous
- Blocking send -- the sender is blocked until the message is received
- Blocking receive -- the receiver is blocked until a message is available

Non-blocking is considered asynchronous
- Non-blocking send -- the sender sends the message and continue
- Non-blocking receive -- the receiver receives: A valid message, or Null message