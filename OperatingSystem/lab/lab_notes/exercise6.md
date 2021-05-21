# Lab exercise 6 - fork(), exit(), exec()


<br>

### fork() system call

```c
asd@b10s:~/Desktop/oslab$ cat fork.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        if(fork() == 0)
        {
                printf("Good day!\n");
        }

        printf("awesome\n");
        return 0;
}
asd@b10s:~/Desktop/oslab$ ./fork 
awesome
Good day!
awesome
```

<br>

```c
// modified
asd@b10s:~/Desktop/oslab$ cat fork.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        if(fork() == 0)
        {
                printf("child!\n");
        }

        else
        {
                printf("parent!\n");
        }

        return 0;
}

asd@b10s:~/Desktop/oslab$ ./fork 
parent!
child!
asd@b10s:~/Desktop/oslab$ ./fork 
parent!
child!

```

<br>

```bash
# modified again

asd@b10s:~/Desktop/oslab$ cat fork.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        if(fork() == 0)
        {
                printf("child: %d\n", getpid());
        }

        else
        {
                printf("parent: %d\n", getppid());
        }

        return 0;
}
asd@b10s:~/Desktop/oslab$ ./fork 
parent: 1548
child: 2101
asd@b10s:~/Desktop/oslab$ ./fork 
parent: 1548
child: 2103

```

<br>

### exit() system call

```bash
asd@b10s:~/Desktop/oslab$ cat exit.c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>  // for exit()

int main()
{
        pid_t process = fork();

        if(process == 0)
        {
                printf("child exiting!\n");
                exit(0);
        }

        else
        {
                printf("parent not exiting\n");
        }


        return 0;
}
asd@b10s:~/Desktop/oslab$ ./exit
parent not exiting
child exiting!

```

<br>

```bash
# modified

asd@b10s:~/Desktop/oslab$ cat exit.c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>  // for exit()

int main()
{
        pid_t process = fork();

        if(process == 1)  // changing it here
        {
                printf("child exiting!\n");
                exit(0);
        }

        else
        {
                printf("parent not exiting\n");
        }


        return 0;
}
asd@b10s:~/Desktop/oslab$ ./exit
parent not exiting
parent not exiting

```

<br>

```bash
# modified again

asd@b10s:~/Desktop/oslab$ cat exit.c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>  // for exit()

int main()
{
        pid_t process = fork();

        if(process == 0)
        {
                printf("child exiting with pid: %d!\n", getpid());
                exit(0);
        }

        else
        {
                printf("parent not exiting with ppid: %d\n", getppid());
        }


        return 0;
}


asd@b10s:~/Desktop/oslab$ ./exit
parent not exiting with ppid: 1548
child exiting with pid: 2036!

```

<br>

### exec() system call

```bash
asd@b10s:~/Desktop/oslab$ cat exec.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        printf("You are running exec.c with pid: %d\n", getpid());

        char *args[] = {"./hello", NULL};

        execv(args[0], args);

        printf("This line is not printed since it does not reach here!");
        // the above line will be printed iff the return value of execv != 0

        return 0;
}

asd@b10s:~/Desktop/oslab$ cat hello.c
#include <stdio.h>
#include <unistd.h>

int main()
{
        printf("This is hello.c program and pid is: %d\n", getpid());
        return 0;
}
asd@b10s:~/Desktop/oslab$ ./exec 
You are running exec.c with pid: 1679
This is hello.c program and pid is: 1679

# notice the same pid value
```

<br>

### some other examples

```bash
asd@b10s:~/Desktop/oslab/execFile$ cat exec.c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        execlp("ping", "ping", "1.1.1.1" , NULL);

        printf("Program finished running!");
        return 0;
}

asd@b10s:~/Desktop/oslab/execFile$ ./exec 
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=128 time=708 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=128 time=44.6 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=128 time=31.0 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=128 time=40.6 ms
^C
--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3010ms
rtt min/avg/max/mdev = 31.043/206.132/708.330/289.985 ms


asd@b10s:~/Desktop/oslab/execFile$ cat exec.c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        execlp("pin", "ping", "1.1.1.1" , NULL);  
		// made an error in "ping" to see what happens

        printf("Program finished running!");
        return 0;
}

asd@b10s:~/Desktop/oslab/execFile$ ./exec 
Program finished running!
```

<br>

```bash
# modified the program

asd@b10s:~/Desktop/oslab/execFile$ cat exec.c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        char *args[] = {"ping", "1.0.0.1", NULL};
        execvp(args[0], args);

        printf("Program finished running!");
        return 0;
}

asd@b10s:~/Desktop/oslab/execFile$ ./exec 
PING 1.0.0.1 (1.0.0.1) 56(84) bytes of data.
64 bytes from 1.0.0.1: icmp_seq=1 ttl=128 time=49.5 ms
64 bytes from 1.0.0.1: icmp_seq=2 ttl=128 time=52.5 ms
^C
--- 1.0.0.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1008ms
rtt min/avg/max/mdev = 49.533/51.026/52.520/1.493 ms


# modified with hello program which lies the previous directory
asd@b10s:~/Desktop/oslab/execFile$ ./exec 
This is hello.c program and pid is: 2106
asd@b10s:~/Desktop/oslab/execFile$ cat exec.c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        char *args[] = {"../hello", "1.0.0.1", NULL};
        execvp(args[0], args);

        printf("Program finished running!");
        return 0;
}
asd@b10s:~/Desktop/oslab/execFile$ ./exec 
This is hello.c program and pid is: 2110



```

<br>

**notes -** 
1. The exec family of functions replaces the current running process with a new process. It can be used to run a C program by using another C program. It comes under the header file *unistd.h*.
2. for suffix having 'v' in the exec family - The arguements are presented as a string of array. Also, the array of pointers must be terminated by a null pointer.
3. for suffix having 'p' in the exec family - specifies that path of the executable used.
4. for suffix having 'l' (small 'L') in the exec family - the arguements are as a list.
5. The fork system call returns 0 if child forked is successful, 1 (non-zero number) for parent, and -ve number for process failed.


<br>

resources - 
- [GFG](https://geeksforgeeks.org)
- [CodeVault YT](https://www.youtube.com/channel/UC6qj_bPq6tQ6hLwOBpBQ42Q)

---

# fork
when a child gets created, it's fork id = 0 and the parent id != 0.

What happens when you call fork() multiple times? It creates 2^n number of forks. And watch [this](https://www.youtube.com/watch?v=94URLRsjqMQ&list=PLfqABt5AS4FmErobw8YyTwXDUE5nPH5lH&index=121)
