## ps cmd

```bash
$ ps --help simple  # ps --help will show about what ind of help you want - list, simple
$ ps -f  # notice PID and PPID
$ ps -l
$ ps -L  # memory % and CPU
$ ps -A -o 'user,pid,vsize'  # to check for a specific process's memory consumption
```

-20 is the highest priority, 19 is the lowest priority

```bash
$ kill -l  # then use the signall number 9 to kill the application

$ kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX


$ bg  # shows bg processes  
$ sleep 1000 &  # ampersand sends the process to the background
$ $fg  # brings the recent bg process to goreground

$ nice -n -20 sleep 5000 &  # changes to highest priority of the `sleep 5000` process.


# renice -n <priority_num> -p <pid>
$ renice -n 10 -p 3088
```
---

## Process scheduling

**at command**

$ at

Executes commands at a specified time.

- Open an `at` prompt to create a new set of scheduled commands, press `Ctrl + D` to save and exit:
  at hh:mm

- Execute the commands and email the result using a local mailing program such as sendmail:
  at hh:mm -m

- Execute a script at the given time:
  at hh:mm -f path/to/file

- Display a system notification at 11pm on February 18th:
  echo "notify-send 'Wake up!'" | at 11pm Feb 18