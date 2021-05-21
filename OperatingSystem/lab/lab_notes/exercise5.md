# Lab exercise 5 - processes, cron


1.  Move a foreground process to back ground and list the back ground processes that are running.

```bash
asd@b10s:~$ jobs
asd@b10s:~$ ping 1.0.0.1 > /dev/null   # > /dev/null redirects the output to null.
^Z
[1]+  Stopped                 ping 1.0.0.1 > /dev/null
asd@b10s:~$ jobs
[1]+  Stopped                 ping 1.0.0.1 > /dev/null
asd@b10s:~$ bg
[1]+ ping 1.0.0.1 > /dev/null &
asd@b10s:~$ jobs
[1]+  Running                 ping 1.0.0.1 > /dev/null &

```

 note -> `/dev/null` is a data sink file (easier way to understand - it's like a blackhole, i.e, it can take in anything but not give out).
 
---

2.  Move a background process to foreground.

```bash
asd@b10s:~$ jobs
[1]+  Running                 ping 1.0.0.1 > /dev/null &
asd@b10s:~$ fg
ping 1.0.0.1 > /dev/null

```

---

3.  Execute the command to show the processes running by root user.

```bash
# U -> flag for showing processes of a specific user

asd@b10s:~$ top U root
top - 17:21:37 up 20 min,  2 users,  load average: 0.04, 0.05, 0.07
Tasks: 245 total,   1 running, 243 sleeping,   1 stopped,   0 zombie
%Cpu(s):  0.2 us,  0.5 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1355.0 total,     67.6 free,    523.9 used,    763.5 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    666.4 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                        
      1 root      20   0  168880  12972   8480 S   0.0   0.9   0:02.52 systemd                           
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.01 kthreadd                          
      3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp                            
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par_gp           
      9 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 mm_percpu_wq                      
     10 root      20   0       0      0      0 S   0.0   0.0   0:00.06 ksoftirqd/0                       
     11 root      20   0       0      0      0 I   0.0   0.0   0:00.38 rcu_sched                    
```

---

4.  List the memory usage of running processes along with user name and Process ID.

```bash
asd@b10s:~$ ps -o pid,user,%mem
    PID USER     %MEM
   3054 asd       0.3
   3249 asd       0.2
```

---

5.  List the memory usage of running processes along with user name and Process ID.

- User
- PID
- Memory Usage %
- Size of the virtual memory
- CPU Utilization
- Start time
- Status

```bash
# the 'u' flag is user-oriented format and is under 'ps --help output'
asd@b10s:~$ ps u
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
asd         2475  0.0  0.3  10920  5440 pts/2    Ss+  17:16   0:00 /bin/bash
asd         2481  0.0  0.0   9692   928 pts/2    T    17:16   0:00 ping 1.0.0.1
asd         2996  0.0  0.1   2640  1752 pts/2    T    17:38   0:00 at 05:39
asd         3054  0.0  0.3  10788  4956 pts/3    Ss   17:45   0:00 /bin/bash
asd         3082  0.0  0.2  11492  3292 pts/3    R+   17:48   0:00 ps u
```

---

6. Demonstrate the usage of NICE and RENICE command

```bash
# ran the cmd as root
root@b10s:~# nice -n -15 ping 1.0.0.1

# top cmd running on another terminal - only some process shown here
asd@b10s:~$ top
top - 08:06:40 up 3 min,  1 user,  load average: 0.11, 0.21, 0.10
Tasks: 286 total,   1 running, 285 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.5 us,  1.5 sy,  0.0 ni, 98.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1355.0 total,    287.5 free,    495.0 used,    572.5 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    701.3 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND          
   1543 asd       20   0   11984   4060   3320 R   0.3   0.3   0:00.25 top              
   1527 root       5 -15    9692    928    804 S   0.0   0.1   0:00.07 ping             
   1520 root      20   0    9836   3932   3404 S   0.0   0.3   0:00.00 bash 

# this shows that the nice value was set successfully


root@b10s:~# renice -n 5 -p 1527  # pid value of process = 1527
1527 (process ID) old priority -15, new priority 5

asd@b10s:~$ top
top - 08:19:19 up 16 min,  1 user,  load average: 0.03, 0.05, 0.07
Tasks: 258 total,   1 running, 257 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.5 sy,  0.0 ni, 99.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1355.0 total,    252.8 free,    524.6 used,    577.6 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    669.6 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                    
   1545 asd       20   0  398900  74056  60320 S   0.0   5.3   0:00.52 qterminal        
   1543 asd       20   0   11984   4060   3320 R   0.0   0.3   0:01.65 top              
   1527 root      25   5    9692    928    804 S   0.0   0.1   0:00.46 ping 

```


          
<br>

**Optional Questions**

7.  Compile and Display the output of any C code by every two minutes using crontab

```bash
*/2 * * * * ~/Desktop/oslab/cfile >> /dev/pts/1
```
---

8.  Display the message in another terminal for every minutes using crontab.

```bash
* * * * * echo message >> /dev/pts/2
```

---

9.  Create a Cronjob for the user ‘Sam’ that runs /bin/date daily at 12:18pm and redirects the output to /home/sam/stamp

```bash
18 12 * * * /usr/bin/date >> /home/sam/stamp
```


---

10.  The user ‘Rithul’ should configure a cron job that runs daily @ 12:15PM local time and executes:/bin/echo Date

```bash
15 12 * * * /usr/bin/date | xargs /usr/bin/echo >> /dev/pts/1
```

---

11.  Schedule Multiple Jobs using ‘at’ command

```bash
asd@b10s:~$ at 17:52
warning: commands will be executed using /bin/sh
at> echo hello > /dev/pts/2
at> /usr/bin/date | xargs /usr/bin/echo > /dev/pts/2
at> cd ~/Desktop && mkdir folder
at> <EOT>
job 6 at Sun Feb 21 17:52:00 2021
asd@b10s:~$ 
asd@b10s:~$ hello
Sunday 21 February 2021 05:52:00 PM IST
^C
asd@b10s:~$ cd Desktop/
asd@b10s:~/Desktop$ ls -l folder/
total 0

# therefore, the at command ran successfully.

```


---

### Notes -
1. To run a command in the background, add the ampersand symbol (`&`) at the end of the command.

```bash
command &
```

2. for nice and renice cmds -> [techmint.com](https://www.tecmint.com/set-linux-process-priority-using-nice-and-renice-commands/)
3. `jobs` prints background processes running on.
4. To put a process to bg, first stop it using `ctrl + z` and then type `bg` -> type `jobs` to check if it running the the bg successfully.

