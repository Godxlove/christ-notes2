# Lab exercise 4 - grep


First of all, let us look at the contents of demo.txt:
```bash
$ cat demo.txt 
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
This Line Has All Its First Character Of The Word With Upper Case.
omg, great.
OMG, WOW.


Two lines above ThIs line is empty.
And tHiS is the last line.
Say hello!

```

---

### Commands used --> grep with flags: -i, -o, -e, -n, -w, -r, -v

grep --> Matches patterns in input text.
syntax --> grep  [options] search_pattern path/to/file

<br>

**grep -i**
- grep -i "this" demo.txt
- grep -i "omg" demo.txt 

```bash
# -i flag show the word "this" irrespective of the case (small/capital)
$ grep -i "this" demo.txt 
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
This Line Has All Its First Character Of The Word With Upper Case.
Two lines above ThIs line is empty.
And tHiS is the last line.

$ grep -i "omg" demo.txt 
omg, great.
OMG, WOW.

# -i is also written as --ignore-case

```

---

**grep -o**
- grep -o "this" demo.txt
- grep -o "this" demo.txt

```bash
# -o prints only the matched parts of a matching line, with each such part on a separate output line.

$ grep -o "omg" demo.txt 
omg

$ grep -o "this" demo.txt 
this
this

$ grep -io "this" demo.txt  # notice the -i flag
THIS
THIS
this
this
This
ThIs
tHiS

# -o is also written as --only-matching
```

---

**grep -e**
- grep -e "hello" -e "case" demo.txt 
- grep -e "hello" -e "omg"  demo.txt 


```bash
# permission for multiple expressions

$ grep -e "hello" -e "case" demo.txt 
this line is the 1st lower case line in this file.
Say hello!

$ grep -e "hello" -e "omg"  demo.txt 
omg, great.
Say hello!

$ grep -e "Case" demo.txt 
This Line Has All Its First Character Of The Word With Upper Case.

# -e PATTERNS, --regexp=PATTERNS
```

---

**grep -n**
- grep -n "case" demo.txt 
- grep -n "this" demo.txt

```bash
# -n prefixes each line of output with line numbers which matches the expressions. 
# It shows matching line [n]umbers

$ grep -n "case" demo.txt 
2:this line is the 1st lower case line in this file.

$ grep -n "this" demo.txt 
2:this line is the 1st lower case line in this file.

$ grep -n "This" demo.txt 
3:This Line Has All Its First Character Of The Word With Upper Case.

$ grep -ni "case" demo.txt  # notice the -i flag
1:THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
2:this line is the 1st lower case line in this file.
3:This Line Has All Its First Character Of The Word With Upper Case.

# -n, --line-number

```

---

**grep -w**
- grep -w "THIS" demo.txt 
- grep -w "THI" demo.txt 

```bash
# -w prints lines which match the exact pattern (word)

$ grep -w "THIS" demo.txt 
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.

$ grep -w "THI" demo.txt  # gives no output

$ grep -w "line" demo.txt 
this line is the 1st lower case line in this file.
Two lines above ThIs line is empty.
And tHiS is the last line.

$ grep -w "lin" demo.txt # gives no output

# comparing grep without -w flag
$ grep "lin" demo.txt 
this line is the 1st lower case line in this file.
Two lines above ThIs line is empty.
And tHiS is the last line.

# -w, --word-regexp

```

---

**grep -r**
- grep -r "case" demo.txt
- grep -r "case"
- grep -ir "case"

```bash
# -r flag reads all the files under each directly recursively.
# if no file is given, it searches in currently directory.

$ grep -r "case" demo.txt
this line is the 1st lower case line in this file.

$ grep -r "case"
hello.txt:this file is not case sensitive haha!
demo.txt:this line is the 1st lower case line in this file.

$ grep -ir "case"  # -i flag included too
hello.txt:this file is not case sensitive haha!
demo.txt:THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
demo.txt:this line is the 1st lower case line in this file.
demo.txt:This Line Has All Its First Character Of The Word With Upper Case.

# -r, --recursive

```
---

**grep -v**
- grep -v "case" demo.txt
- grep -vi "case" demo.txt


```bash
# -v flag inverts the sense of matching, to select non-matching lines.
# so whichever line does not have the "word", it displays that.

$ grep -v "case" demo.txt  # case sensitive
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
This Line Has All Its First Character Of The Word With Upper Case.
omg, great.
OMG, WOW.


Two lines above ThIs line is empty.
And tHiS is the last line.
Say hello!

$ grep -vi "case" demo.txt  # -i turns into case insensitive
omg, great.
OMG, WOW.


Two lines above ThIs line is empty.
And tHiS is the last line.
Say hello!


# -v, --invert-match

```


---

### ii) Write the appropriate UNIX/Linux commands for the following questions
1. Delete the empty files in the current working directory
- $ find . -type f -empty -exec rm {} \\;

<br>

2. Display all the files and directories which has read and write permission only.
- $ find . -perm /600
- $ find . -perm -600
- $ find . -perm -u=rw

<br>

3. Delete the files which consume exactly 1MB space in the given directory
- $ find . -type f -size 1M -exec rm {} \\;

```bash
$ ls
demo1.txt  demo.txt  read1  read.txt  text  write1  write.txt
$ find . -type f -size 1M -exec rm {} \;
$ ls
read1  read.txt  text  write1  write.txt

```

<br>

4. Delete the empty folders
- $ find . -type f -empty -exec rm {} \\;

```bash
$ ls
read1  read.txt  text  write1  write.txt
$ find . -type f -empty -exec rm {} \;
$ ls
read1  text  write1

```

<br>

5. Move empty directories to the new directory called ‘empty’
- $ find . -type d -empty -exec mv {} ./empty \\;

<br>

6. Delete the files for the given directory which older than 10 days
- $ find . -type f -mtime +10 -exec rm {} \\;

```
here, +10 = file more than 10 days old
-10 = file less than 10 days old
10 = file exactly 10 days old
```
reference - [stackoverflow](https://stackoverflow.com/questions/25599094/explaining-the-find-mtime-command)

<br>

7. Display Hidden files in your current working directory
- $ find . -iname ".*"

<br>

8. Display the files and directories which doesn’t have 777 permissions
- $ find . ! -perm -777

"!" implies "not".

<br>

9. Find and display the files which are modified 25 days back from the disk
- $ find . -type f -mtime 25

<br>

10. Display the empty files and directories every 15 minutes (900 seconds).
- $ find . -empty -exec watch -n 900 cat {} \\;

This above command (watch) shows output in a full screen. Cron job would've been better for this task.

<br>

```bash
# shows the words starting with 'm' -> regular expressions
$ grep -i ^m test.txt
```

<br>

#### Some epic references -
1. [difference between -exec rm and -delete](https://unix.stackexchange.com/questions/167823/finds-exec-rm-vs-delete)
2. TomNomNom's thread on [find](https://mobile.twitter.com/TomNomNom/status/1269263730992439296) cmd.
3. Some notes on find cmd in [Github](https://github.com/imran-parray/Publicly-shared-notes/blob/master/find_command_notes.md).