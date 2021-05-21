# OS Lab Assignment Solutions
### Create three following directories:

-   Sports    
-   Entertainment
-   Education
    
<br>

### Create the following -
-   three sub-directories called **Cricket, Football** and **Tennis** inside ‘Sports’
-   two sub-folders as **Movies, Social Media** inside the directory called ‘Entertainment’
-   two sub-directories named as **University** and **College** inside ‘Education’
    

Each sub-directories should have minimum three relevant files with appropriate contents and execute the following UNIX commands in the terminal and store the output in the file called **“UnixLab1.txt”**

1.  Write a UNIX Command to display the permission of all sub-directories
- ls -lR
    
2.  Write a UNIX Command to display the files which starts with the particular character for the given directory
- ls E*
    
3.  Write a UNIX Command to display the content of the file along with line number
- cat -n Christ_uni.txt 

4.  Write a UNIX Command to display all the files along with the name of its sub-directories
- ls -R
    
5.  Write a UNIX Command to display the sub-directories in alphabetical order
- ls Education/ Entertainment/ Sports/
    
6.  Write a UNIX Command to copy Sports directory along with its sub-directories to the newly created folder called ‘Game’’
- cp -R Sports/ ./Game
    
7.  Write a UNIX Command to display the file contents in reverse order
- tac sania_mirza.txt 

8.  Write a UNIX Command to hide and unhide the files
- mv sania_mirza.txt ./.sania_mirza.txt

9.  Write a UNIX Command to sort the files by file size
- ls -laS

10.  Write a UNIX Command to print the file size of all sub-directories in units other than byes
- ls -laSh

11.  Write a UNIX Command to display first and last line of the file
- head -n 1 martina_hingis.txt && tail -n 1 martina_hingis.txt 

12.  Write a UNIX Command to display the 2nd line to 5th line for the given file
- sed -n '2,5p' martina_hingis.txt 

13.  Delete any sub-directories where the files are not empty
- rm -r Game/

14.  Write a UNIX Command to sort and merge the contents of three files in Cricket and store the output content to the file called ‘merge.txt’

<br>

cat < what_is_cricket.txt >> merge.txt
cat < tendulkar.txt >> merge.txt
cat < virat.txt >> merge.txt
cat merge.txt 


15.  Write a UNIX Command not to add content to the existing file
- chmod u-w tendulkar.txt 
