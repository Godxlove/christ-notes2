# Lab exercise 7 - zombie, orphan, child processes.


<br>

1. Design a program to demonstrate zombie process.

```bash
# content of zombie.c
asd@b10s:~/Desktop/oslab/zombie$ cat zombie.c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main()
{
        if(fork() == 0)
        {
                printf("child: %d\n", getpid());
        }

        else
        {
                sleep(5);
                printf("parent: %d\n", getppid());
        }

        return 0;
}
asd@b10s:~/Desktop/oslab/zombie$ ./zombie &  # executing zombie in the bg
[1] 1698
asd@b10s:~/Desktop/oslab/zombie$ child: 1699
ps
    PID TTY          TIME CMD
   1504 pts/0    00:00:00 bash
   1698 pts/0    00:00:00 zombie
   1699 pts/0    00:00:00 zombie <defunct>  
   1700 pts/0    00:00:00 ps
asd@b10s:~/Desktop/oslab/zombie$ parent: 1504
ps
    PID TTY          TIME CMD
   1504 pts/0    00:00:00 bash
   1701 pts/0    00:00:00 ps
[1]+  Done                    ./zombie

```

<br>

2. Design a program to demonstrate orphan process  

```bash
asd@b10s:~/Desktop/oslab/zombie$ cat orphan.c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main()
{
        pid_t child_pid = fork();
        if(child_pid == 0)
        {
                sleep(10);
                printf("child: %d\n", getpid());
                printf("my parent pid is: %d\n", getppid());
        }

        else
        {
                sleep(4);
                printf("parent: %d\n", getppid());
                printf("my child is: %d\n", child_pid); 
        }

        return 0;
}

asd@b10s:~/Desktop/oslab/zombie$ gcc orphan.c -o orphan
asd@b10s:~/Desktop/oslab/zombie$ ./orphan &
[1] 1809
asd@b10s:~/Desktop/oslab/zombie$ ps
    PID TTY          TIME CMD
   1504 pts/0    00:00:00 bash
   1809 pts/0    00:00:00 orphan
   1810 pts/0    00:00:00 orphan
   1811 pts/0    00:00:00 ps
asd@b10s:~/Desktop/oslab/zombie$ parent: 1504
my child is: 1810
ps
    PID TTY          TIME CMD
   1504 pts/0    00:00:00 bash
   1810 pts/0    00:00:00 orphan
   1812 pts/0    00:00:00 ps
[1]+  Done                    ./orphan
asd@b10s:~/Desktop/oslab/zombie$ child: 1810
my parent pid is: 1
ps
    PID TTY          TIME CMD
   1504 pts/0    00:00:00 bash
   1813 pts/0    00:00:00 ps


# running top cmd in another terminal
asd@b10s:~$ top
top - 12:29:13 up  1:06,  1 user,  load average: 0.06, 0.05, 0.01
Tasks: 247 total,   1 running, 245 sleeping,   0 stopped,   1 zombie
%Cpu(s):  0.7 us,  1.5 sy,  0.0 ni, 97.3 id,  0.0 wa,  0.0 hi,  0.5 si,  0.0 st
MiB Mem :   1635.0 total,    490.1 free,    526.7 used,    618.2 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    943.3 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                            
    706 root      20   0  292916  81396  46224 S   2.3   4.9   0:11.70 Xorg                               
   1647 asd       20   0  401748  77208  62792 S   1.7   4.6   0:02.54 qterminal                          
    527 root      20   0    8296   4788   1660 S   0.3   0.3   0:00.72 haveged                            
    992 root      20   0  160828  13596  11188 S   0.3   0.8   0:06.44 vmtoolsd                           
   1501 asd       20   0  409392  76960  62684 S   0.3   4.6   0:09.74 qterminal                          
   2033 asd       20   0   11984   3892   3120 R   0.3   0.2   0:00.05 top                                
      1 root      20   0  102176  11508   8380 S   0.0   0.7   0:02.94 systemd                
```

<br>

3. Write a C Program to write the content called "Welcome to 2BCA-A Class" in the background .

```bash
asd@b10s:~/Desktop/oslab/zombie/question3$ cat bg_file.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        printf("You are running exec.c with pid: %d\n", getpid());

        char *args[] = {"./script.sh", NULL};

        execv(args[0], args);

        printf("This line is not printed since it does not reach here!");
        // the above line will be printed iff the return value of execv != 0

        return 0;
}
asd@b10s:~/Desktop/oslab/zombie/question3$ cat script.sh 
#!/usr/bin/bash

for i in {1..10}
do
        echo Welcome to 2BCA-A Class >> /dev/pts/1
done
asd@b10s:~/Desktop/oslab/zombie/question3$ gcc bg_file.c -o bg_file
asd@b10s:~/Desktop/oslab/zombie/question3$ ./bg_file &
[1] 2266
asd@b10s:~/Desktop/oslab/zombie/question3$ You are running exec.c with pid: 2266


# in /dev/pts/1 terminal
asd@b10s:~/Desktop$ tty
/dev/pts/1
asd@b10s:~/Desktop/$ Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class
Welcome to 2BCA-A Class

```


<br>

4. Write a C program in UNIX platform that creates five processes. The original process creates two children processes and then prints out “parent”. The children processes print “child1” and “child2” respectively. The first child creates a child process that prints out “grandchild1” and the second child process creates a child process that prints out “grandchild2”. Each process should print out its process id and the process id of its parent. The original process should wait until all the child process terminates.

```bash
asd@b10s:~/Desktop/oslab/zombie/granchild$ cat granchild.c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
        pid_t child1 = fork();
        pid_t child2 = fork();

        if(child1 == 0)
        {

                pid_t grand1 = fork();

                if(grand1 == 0)
                {
                        printf("\n\n\tGrandchild 1");
                        printf("\npid of Grandchild 1: %d",getpid());
                        printf("\npid of Child 1 : %d\n",getppid());
                }

                else
                {
				 		wait(NULL);
                        printf("\n\n\tChild 1\n");
                        printf("pid of Child 1: %d",getpid());
                        printf("\npid of Parent: %d\n",getppid());
                }

        }

        if(child2 == 0)
        {

                pid_t grand2 = fork();

                if(grand2 == 0)
                {
                        printf("\n\n\tGrandchild 2");
                        printf("\npid of Grandchild 2: %d",getpid());
                        printf("\npid of Child 2: %d\n",getppid());
                }

                else
                {
				 wait(NULL);
                        printf("\n\n\tChild 2\n");
                        printf("pid of Child 2: %d",getpid());
                        printf("\npid of Parent: %d\n",getppid());
                }
        }

        else
        {   
                wait(NULL);
                printf("\n\n\tParent process\n");
                printf("pid of Parent: %d\n",getpid());
        }
return(0);
}
asd@b10s:~/Desktop/oslab/zombie/granchild$ 

        Grandchild 2
pid of Grandchild 2: 2351
pid of Child 2: 2350


        Child 2
pid of Child 2: 2350
pid of Parent: 2347


        Child 1
pid of Child 1: 2347
pid of Parent: 2345


        Grandchild 2
pid of Grandchild 2: 2352
pid of Child 2: 2347


        Child 2
pid of Child 2: 2347
pid of Parent: 2345


        Parent process
pid of Parent: 2345
        Grandchild 2
pid of Grandchild 2: 1576
pid of Child 2: 1575
pid of Parent: 1569
asd@b10s:~/Desktop/oslab/zombie/granchild$ 

        Child 2
pid of Child 2: 1575
pid of Parent: 1572


        Child 1
pid of Child 1: 1572
pid of Parent: 1570


        Grandchild 2
pid of Grandchild 2: 1577
pid of Child 2: 1572


        Child 2
pid of Child 2: 1572
pid of Parent: 1570


        Parent process
pid of Parent: 1570
```

---

notes: [process-termination](process-termination.md)
1. When the child process is finished, but the parent doesn't know about it. The child process can be seen the the `ps`  cmd. The child is the zombie.
2. In order to prevent creating zombie processes, add `wait(NULL)` in the code of the parent process. This will make the parent wait before the child finishes.
3. defunct meaning from the man pages- Processes marked **`<defunct>`** are dead processes (so-called _"zombies"_) that remain because their parent has not destroyed them properly. These processes will be destroyed by init(8) if the parent process exits. 
4. Orphan processes are those processes that are still running even though their parent process has terminated or finished.

---

stuff found out:
1. how `/usr/bin/env bash` and `/bin/bash` differs [here](https://stackoverflow.com/questions/16365130/what-is-the-difference-between-usr-bin-env-bash-and-usr-bin-bash) and long answer [here](https://unix.stackexchange.com/questions/29608/why-is-it-better-to-use-usr-bin-env-name-instead-of-path-to-name-as-my).

tags - #zombie #orphan #wait