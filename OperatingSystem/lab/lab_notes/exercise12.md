# Lab exercise 12 - Threads


### Code
```c

// header files
#include <stdio.h>
#include <unistd.h>
#include <pthread.h>


// function declarations
int fibonacci(int);

void *fibonacci_runner(void *arg)
{
	int *num = (int *) arg;
	int i, result;
	
	i = result = 0;
	
	printf("\nThread 1..");
	if (*num < 1)
    {
    	printf("\nThe number cannot be negative or zero for fibonacci!");
    }
	
	else
	{
		printf("\nFibonacci series: ");
		
		for (i = 0; i < *num; i++)
		{
			result = fibonacci(i);
			printf("%d ", result);
		}
	}
	
	// return NULL;
	pthread_exit(0);	
}

void *factorial_runner(void *arg)
{
	int *num = (int *) arg;
	int i;
	long long last;
	
	i = last = 1;
	printf("\n\nThread 2...\n");
	
	if(*num < 0)
	{
		printf("\nThe factorial of a negative number doesn't exist! \n");
	}
	
	else if (*num == 0)
	{
		printf("\nThe factorial of zero is: 1\n");
	}
	
	else
	{
		for (i = 1; i < *num; i++)
		{
			last *= i;
		}
		
		printf("The factorial of %d is: %lld \n", *num, last);
	
	}

	pthread_exit(0);
}


int main()
{
	int num;
	
	// thread id creation
	pthread_t tid, tid2;
	
	// for fibonacci series
    printf("\n(For fibonacci series)\nEnter a number: ");
    scanf("%d", &num);    
    
    // for factorials
    printf("\n(For factorials)\nEnter a number: ");
    scanf("%d", &num);
    
    
    // creating threads for fibonacci series
    pthread_create(&tid, NULL, fibonacci_runner, &num);
    
    // creating threads for factorials
    pthread_create(&tid2, NULL, factorial_runner, &num);
    
    
    pthread_join(tid, NULL);
    pthread_join(tid2, NULL);
    
    return 0;
}



int fibonacci(int num)
{
	if (num <= 1)
		return num;
	
	else
		return fibonacci(num - 1) + fibonacci(num - 2);
}
```

<br>

#### Compiling and Working

```bash
meow@pop-os:~/Public/oslab/lab12-threads$ make
gcc -Wall -Wextra -pthread thread.c -o thread
meow@pop-os:~/Public/oslab/lab12-threads$ ./thread 

(For fibonacci series)
Enter a number: 12

(For factorials)
Enter a number: 5

Thread 1..
Fibonacci series: 0 1 1 2 3 

Thread 2...
The factorial of 5 is: 24 
meow@pop-os:~/Public/oslab/lab12-threads$ ./thread 

(For fibonacci series)
Enter a number: 16

(For factorials)
Enter a number: 10

Thread 1..
Fibonacci series: 0 1 1 2 3 5 8 

Thread 2...
The factorial of 10 is: 362880
```


# Resources
- Where to use pthread_exit() - [here](https://www.bo-yang.net/2014/11/20/pthread_exit-in-main) and [google groups](https://groups.google.com/forum/#!topic/comp.programming.threads/b1r0oUwG4rM)