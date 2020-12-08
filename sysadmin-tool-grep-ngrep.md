# grep

grep [options] pattern path_to_search

grep -HRni

grep [0-9] <filename> 		Print the lines that contain the numbers 0 through 9

grep [0,1,2,3,4,5] <filename>  	Print the lines that contain the numbers 0–5 in a file

grep -C 3 [pattern] <filename> 	Print context of lines (specified number of lines above and below the pattern) for matching the pattern. Here, the number of lines is specified as 3.


# egrep grep OR

```
grep "PATTERN1\|PATTERN2" file
grep -E "PATTERN1|PATTERN2" file
grep -e PATTERN1 -e PATTERN2 file
egrep "PATTERN1|PATTERN2" file
```

# grep AND

```
grep "this" | grep "and this"

grep -E 'this*and this' filename
```


# grep inverting pattern

-v or --invert-match Print all lines that do not match the pattern

grep -v [pattern] <filename>




# strings

strings is used to extract all printable character strings found in the file or files given as arguments. It is useful in locating human-readable content embedded in binary files; for text files one can just use grep.

$ strings book1.xls | grep my_string


# ngrep - network grep
