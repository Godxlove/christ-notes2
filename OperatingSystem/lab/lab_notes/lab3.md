```sh
find . -type f -empty -exec rm -f {} \\;
```
a find command

<br>

grep, du

grep -v -e "lower" -e "UPPER" file.txt
grep -i will switch off the case sentitive
-o will display only the word searched

![](grep_egs.png)
cap (^) - beginning
dollar ($) - end