[this is some good note](https://condor.depaul.edu/glancast/343class/hw/hw4ans.html) along with [this](https://condor.depaul.edu/glancast/343class/hw/hw3ans.html) (idk why I put this).

---

## Notes on CPU scheduling algo

#### FCFS (first come first serve)
reference [video](https://youtu.be/WYo1SpUh9FI) and [this](https://youtu.be/MZdVAVMgNpA)
1. it is a non-preemptive algo.
2. assigns CPU to the first process which comes in (criteria is "arrival time")
3. The process order matter when there are two processes having the same arrival time. (choose the first one which appears in the list)
4. WAITING TIME = RESPONSE TIME (non-preemptive)

Columns to be made -
process no., arrival time, burst time, completion time, turn around time, waiting time, response time

**May ask about** avg turn around time and avg waiting time.


----

<br>

#### SJF non-preemptive (Shortest Job First)
reference [video](https://youtu.be/VCIVXPoiLpU) and [this](https://youtu.be/pYO-FAg-TpQ)
1. it is a non-preemptive algo (a process once executed will not be interrupted untill it is over)
2. assigns CPU to the process which has the least burst time (**criteria is "burst time"**) - but do check the arrival time.
3. The arrival time matters when there are two processes having the same burst time. If both arrival and burst time as same then choose the process number order.
4. WAITING TIME = RESPONSE TIME (non-preemptive)

Columns to be made -
process no., arrival time, burst time, completion time, turn around time, waiting time, response time

May ask about avg turn around time and avg waiting time.

<br>

---

#### # Shortest Remaining Time First (SRTF) = SJF preemptive
reference [video](https://youtu.be/_QcX99B-zbU) and [this](https://youtu.be/pYO-FAg-TpQ)
1. it is a preemptive algo (a process executing can be interrupted in place of a more important process)
2. assigns CPU to the process which has the least burst time (**criteria is "burst time"**) - but do check the arrival time.
3. The arrival time matters when there are two processes having the same burst time. If both arrival and burst time as same then choose the process number order.
4. WAITING TIME = RESPONSE TIME (non-preemptive)

Columns to be made -
process no., arrival time, burst time, completion time, turn around time, waiting time, response time

May ask about avg turn around time and avg waiting time.





<br>

---

Read from sir's notes given below and practice them using question from [assignment-async](assignment-async.md). Gayathri's solutions are there to check if you have done it correctly.

<br>

![](CPU-Process-Scheduling-Solved-Problems.pdf)