```sh
touch text_file{1..10}.txt
```
makes files from text_file1, text_file2 ...till text_file10.

<br>

```sh
rm -i text_file{1..10}.txt
```
this switch (-i) prompts before every removal of the files.

```sh
cat file1.txt file2.txt >> file.txt
```
appends the contents of file1.txt and file2.txt into file.txt

<br>

extundelete, testdisk - enable to use undo command

<br>

```sh
script start.txt

exit # (to quit)
```
This stores every command you use.

---

```sh
size <exe_file>
```
size maps out the memory layout of your C program.
bss - block state symbol - depends on cpu architecture - 32/64

---

![](system_calls_by_program.png)

strace ./exe_file
-> shows the system calls done by the program
```sh
mmap # memory map
```

![](system_calls_by_program.png)

sleep is a method which makes the system wait for seconds by default.
for us, its "printf", but for kernel it is write().

<br>

for us its exe file, for kernel, it is the process id to identify it.

```sh
pidof exe_file
pmap pid_num_of_exe_process
```

![](swapping_by_bitwise_xor.png)

![](strace_on_swapping_program.png)


