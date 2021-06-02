# Terms to know
resource - [afteracademy](https://afteracademy.com/blog/what-is-burst-arrival-exit-response-waiting-turnaround-time-and-throughput)

1. **Burst Time** (aka execution time) is the total time taken by the process for its execution on the CPU.
2. **Arrival time** is the time when a process enters into the ready state and is ready for its execution.
3. **Exit time** is the time when a process completes its execution and exits from the system.
4. **Response time** = time at which the process gets CPU for the first time - arrival time *OR* Response time is the time spent between the ready state and getting the CPU for the first time.
5. **Waiting time** = (total time - burst time) *OR* the waiting time is the total time taken by the process in the ready state.
6. **Turnaround time** is the total amount of time spent by the process from coming in the ready state for the first time to its completion *OR* turnaround time = burst time + time during ready state + I/O time *OR* Turnaround time = (exit time - arrival time).
7. **Throughput** is a way to find the efficiency of a CPU. It can be defined as the number of processes executed by the CPU in a given amount of time. 

Throughput example -> let's say, the process P1 takes 3 seconds for execution, P2 takes 5 seconds, and P3 takes 10 seconds. So, throughput, in this case, the throughput will be (3+5+10)/3 = 18/3 = 6 seconds.

In short, throughput = (total time each process takes / total number of processes)

---

Notes for Grantt chart questions:
1. The I/O time won't be given, so Turnaround time = burst time  + waiting time.
2. In a **Non-preemptive scheduling algo**, WAITING TIME = RESPONSE TIME.

Follow [cpu-scheduling-algo](cpu-scheduling-algo.md) from here.