## process termination - wait, zombie, orphan

Process executes last statement and then asks the operating system to delete it using the exit() system call.
- Returns status data from child to parent (via wait())
- Process’ resources are deallocated by operating system

<br>

### abort() system call
Parent may terminate the execution of children processes using the abort() system call. Some reasons for doing so:
- Child has exceeded allocated resources
- Task assigned to child is no longer required
- The parent is exiting and the operating systems does not allow a child to continue if its parent terminates.

<br>

Some operating systems do not allow child to exists if its parent has terminated. If a process terminates, then all its children must also be terminated.
- cascading (= a succession of processes) termination. All children, grandchildren, etc. are terminated.
- The termination is initiated by the operating system.
 
The parent process may wait for termination of a child process by using the wait() system call. The call returns status information and the pid of the terminated process pid = wait(&status);
• If no parent waiting (did not invoke wait()) process is a **zombie**
• If parent terminated without invoking wait(), process is an **orphan**

---

### Zombie Process:
A process which has finished the execution but still has entry in the process table to report to its parent process is known as a zombie process.

A child process always first becomes a zombie before being removed from the process table. The parent process reads the exit status of the child process which reaps off the child process entry from the process table.

<br>
In other words -> a child becomes zombie when the child is finished but the parent does not know about it, more info in notes section of [exercise7](exercise7.md)

---

### orphan process
A process whose parent process no more exists i.e. either finished or terminated without waiting for its child process to terminate is called an orphan process. However, the orphan process is soon adopted by init process, once its parent process dies.


tags - #zombie #orphan #wait