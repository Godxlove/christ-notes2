# Lab exercise 3

#### Commands used

**chmod**
- chmod 744 dir*
- chmod 000 file1.txt


```bash
$ chmod 744 dir*
$ ls -l
total 12
drwxr--r-- 2 meow meow 4096 Feb  2 11:14 dir1
drwxr--r-- 2 meow meow 4096 Feb  2 11:14 dir2
drwxr--r-- 2 meow meow 4096 Feb  2 11:14 dir3
-rw-rw-r-- 1 meow meow    0 Feb  2 11:14 file1.txt
-rw-rw-r-- 1 meow meow    0 Feb  2 11:14 file2.txt
-rw-rw-r-- 1 meow meow    0 Feb  2 11:14 file3.txt
-rw-rw-r-- 1 meow meow    0 Feb  2 11:14 file4.txt
-rw-r----- 1 meow meow    0 Feb  2 11:14 file5.txt
-rw-rw-r-- 1 meow meow    0 Feb  2 12:07 lab_3.txt
$ chmod 000 file1.txt 
$ ls -l file1.txt 
---------- 1 meow meow 0 Feb  2 11:14 file1.txt

```

---

**chown**
- sudo chown adam file1.txt file2.txt 

```bash
drwxr--r-- 2 meow meow  4096 Feb  2 11:14 dir3
---------- 1 adam meow     0 Feb  2 11:14 file1.txt
-rw-rw-r-- 1 adam meow     0 Feb  2 11:14 file2.txt
-rw-rw-r-- 1 meow meow     0 Feb  2 11:14 file3.txt
-rw-rw-r-- 1 meow meow     0 Feb  2 11:14 file4.txt
-rw-r----- 1 meow meow     0 Feb  2 11:14 file5.txt
```

<br>

- sudo chown adam:ranger file3.txt file4.txt dir1 
```bash
drwxr--r-- 2 adam ranger  4096 Feb  2 11:14 dir1
drwxr--r-- 2 meow meow    4096 Feb  2 11:14 dir2
drwxr--r-- 2 meow meow    4096 Feb  2 11:14 dir3
---------- 1 adam meow       0 Feb  2 11:14 file1.txt
-rw-rw-r-- 1 adam meow       0 Feb  2 11:14 file2.txt
-rw-rw-r-- 1 adam ranger     0 Feb  2 11:14 file3.txt
-rw-rw-r-- 1 adam ranger     0 Feb  2 11:14 file4.txt
```

---

**chgrp**
- sudo chgrp team file5.txt file4.txt 

```bash
-rw-rw-r-- 1 adam ranger     0 Feb  2 11:14 file3.txt
-rw-rw-r-- 1 adam team       0 Feb  2 11:14 file4.txt
-rw-r----- 1 meow team       0 Feb  2 11:14 file5.txt
```

---

**useradd**
- sudo useradd chotu

---

**adduser**
- sudo adduser bheem

---

**addgroup**
- sudo addgroup team
- sudo addgroup ranger

*output from getent group*
```bash
team:x:1004:
ranger:x:1005:
```

---

**userdel** 
- sudo userdel -r adam

-r flag recursively deletes the home directory of adam.

---

**groupdel**
- sudo delgroup --remove-home team

```bash
$ sudo delgroup --remove-home team
Removing group `team' ...
Done.
```

---

**passwd -** 
- passwd

*output*
```bash
adam@pop-os:/home$ passwd
Changing password for adam.
Current password: 
New password: 
Retype new password: 
Bad: new and old password are too similar
New password: 
Retype new password: 
Bad: new password is too simple
New password: 
Retype new password: 
Bad: new password cannot be a palindrome
passwd: Authentication token manipulation error
passwd: password unchanged
```

<br>

*tried again* 

```bash
New password: 
Retype new password: 
passwd: password updated successfully
```

---

**getent -**
- getent group 
 
*output*
```bash
meow:x:1000:
adam:x:1001:
bheem:x:1002:
chotu:x:1003:
```

---

**gpasswd**
- sudo gpasswd team

```bash
$ sudo gpasswd team
Changing the password for group team
New Password: 
Re-enter new password:
```

---

**umask**
- umask
- umask -S
- umask 0007

```bash
adam@pop-os:/home$ umask
0002
adam@pop-os:/home$ umask -S  # prints the perms in human readable format
u=rwx,g=rwx,o=rx
adam@pop-os:/home$ umask 0007
adam@pop-os:/home$ umask
0007
```

<br>

Let's see umask in action

```bash
adam@pop-os:/home$ umask 0477
adam@pop-os:/home$ umask
0477
adam@pop-os:/home$ cd adam/
adam@pop-os:~$ touch file.txt
adam@pop-os:~$ ls -l
total 0
--w------- 1 adam adam 0 Feb  2 15:01 file.txt
adam@pop-os:~$ umask -S
u=wx,g=,o=
adam@pop-os:~$ exit
meow@pop-os:/home$ cd adam/
meow@pop-os:/home/adam$ ls
file.txt
meow@pop-os:/home/adam$ touch cat
touch: cannot touch 'cat': Permission denied  
# this is cuz adam's home directory has not given perms to others to rwx any stuff

```

---

**usermod**
- sudo usermod -a -G team adam
- sudo usermod -a -G ranger,team bheem

```bash
# after getent group cmd
team:x:1004:adam,bheem
ranger:x:1005:bheem
```

"-a" means "add"
the names after "-G" will add the user adam to the group team.

reference - [networkworld.com](https://www.networkworld.com/article/3409781/mastering-user-groups-on-linux.html)