
# OS LAB - TEST 2 - 02.03.2021

1. Design a C program in UNIX platform to demonstrate the following scenario: 

The original process creates two children processes and then prints out “parent”. The children processes print “child1” and “child2” respectively. The “child2” process should compute Fibonacci series for a number given by the user and prints the output. Each process should print out its process id and the process id of its parent. The original process should wait until all the child process terminates. 

```bash
asd@b10s:~/Desktop/midsem/fibonacci$ cat fibo.c
// header files                                       
#include <stdio.h>                                       
#include <unistd.h>                                   
#include <sys/types.h>
#include <sys/wait.h>                                                                                                                                                                     
// functions declarations
int fibonacci(int);


// main function
int main()
{
        pid_t child1, child2;
        int num, limit, i;

        num = i = limit = 0;

        child1 = fork();


        if(child1 == 0)
        {
                printf("\n\tchild1\n");
                printf("child1 pid: %d\n", getpid());
                printf("parent pid: %d\n", getppid());
        }

        child2 = fork();

        if(child2 == 0)
        {
                printf("\n\tchild2\n");
                printf("child2 pid: %d\n", getpid());
                printf("parent pid: %d\n", getppid());

                printf("\n\nEnter a number to compute fibonacci series: \n");
                scanf("%d", &limit);

                printf("\n\nSeries: ");

                for(i = 0; i < limit; i++)
                {
                        num = fibonacci(i);
                        printf("%d ", num);
                }

                printf("\n");

        }

        else
        {
                wait(NULL);
                printf("\n\n\tparent\n");
        }


        return 0;
}


// fibonacci series generator
int fibonacci(int a) 
{ 
   if (a <= 1) 
      return a; 
      
   return (fibonacci(a-1) + fibonacci(a-2)); 
}

```
![](fibo_output.png)

<br>


  

2. Write a C program in UNIX platform to print a message called “2BCA is the best class in CHRIST (Deemed to be University)” in the file name called bca.txt in every five seconds in the background.  (5 Marks)

```bash
asd@b10s:~/Desktop/midsem/secondques$ cat file.c
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
asd@b10s:~/Desktop/midsem/secondques$ cat script.sh 
#!/bin/bash

cd ~/Desktop/midsem/secondques

touch bca.txt

while true
do
        sleep 5
        echo "Welcome to 2BCA-A Class" >> bca.txt
done
```
![](bcaFile.png)

![](script_file.png)

![](script_file_running.png)
  
<br>

3. Write an appropriate UNIX commands for the following questions (5 Marks)

 i) Write a UNIX Command to list the following details of the given process processes, 
-    UID
-    UNAME    
-    PRIORITY
-    %CPU    
-    %MEM

```bash
asd@b10s:~$ ps -o uid,uname,priority,%cpu,%mem
```

![](uid_uname_pri_cpu_mem.png)

<br>
    

ii) List the memory usage of running processes along with user name and Process ID.
```bash
asd@b10s:~$ ps -o pid,%mem,user
```

![](pid_mem_usr.png)

<br>

iii) Execute the command to show the processes running by the root user.
```bash
$ top U root
```

![](top_U_root.png)
 
 <br>

iv) Execute the command to list the different kill signals along with its numerical values.
```bash
$ kill -l
```
![](kill_minux_l.png)

<br>

v) Display the message called ‘Welcome to CIA2 TEST’ in another terminal for every minutes using crontab.
 
 ```bash
 * * * * * echo Welcome to CIA2 TEST >> /dev/pts/1
 ```
 
 ![](crontab_cia2_test.png)
 