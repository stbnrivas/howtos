# cat tac

## cat

´´´bash
cat file1 file2
´´´


´´´bash
cat file1 file2 > file12
´´´


´´´bash
cat > file
´´´

CTRL + D to end



## tac

The tac command (cat spelled backwards) prints the lines of a file in reverse order. (Each line remains the same, but the order of lines is inverted.) The syntax of tac is exactly the same as for cat, as in:


´´´bash
$ tac file
$ tac file1 file2 > newfile
´´´


# echo

The –e option, along with the following switches, is used to enable special character sequences, such as the newline character or horizontal tab.

    \n  represents newline
    \t  represents horizontal tab


# cat and less

´´´bash
$ less <filename>
$ cat <filename> | less
´´´


# head and tail

´´´bash
$ head –n 5 grub.cfg
$ head -5 grub.cfg.
´´´


´´´bash
$ tail -n 15 atmtrans.txt
$ tail -15 atmtrans.txt
´´´


$ tail -f atmtrans.txt






# Viewing Compressed Files

$ zcat compressed-file.txt.gz 			To view a compressed file
$ zless <filename>.gz
or
$ zmore <filename>.gz 				To page through a compressed file
$ zgrep -i less test-file.txt.gz 		To search inside a compressed file
$ zdiff filename1.txt.gz filename2.txt.gz 	To compare two compressed files


´´´bash
$ head –n 5 grub.cfg
$ head -5 grub.cfg.
´´´





# sed & awk

## sed
sed is a powerful text processing tool and is one of the oldest, earliest and most popular UNIX utilities. It is used to modify the contents of a file, usually placing the contents into a new file. Its name is an abbreviation for stream editor.

Specify editing commands at the command line, operate on file and put the output on standard out (e.g., the terminal)
´´´bash
$ sed -e command <filename>
´´´


Specify a scriptfile containing sed commands, operate on file and put output on standard out.
´´´bash
$ sed -f scriptfile <filename>
´´´


sed s/pattern/replace_string/ file 	Substitute first string occurrence in a line
sed s/pattern/replace_string/g file 	Substitute all string occurrences in a line
sed 1,3s/pattern/replace_string/g file 	Substitute all string occurrences in a range of lines
sed -i s/pattern/replace_string/g file 	Save changes for string substitution in the same file



## awk

awk is used to extract and then print specific contents of a file and is often used to construct reports. It was created at Bell Labs in the 1970s and derived its name from the last names of its authors: Alfred Aho, Peter Weinberger, and Brian Kernighan.

    It is a powerful utility and interpreted programming language.
    It is used to manipulate data files, retrieving, and processing text.
    It works well with fields (containing a single piece of data, essentially a column) and records (a collection of fields, essentially a line in a file).


awk ‘command’ var=value file 	Specify a command directly at the command line
awk -f scriptfile var=value file 	Specify a file that contains the script to be executed along with f


The -F option allows you to specify a particular field separator character



awk '{ print $0 }' /etc/passwd 	Print entire file
awk -F: '{ print $1 }' /etc/passwd 	Print first field (column) of every line, separated by a space
awk -F: '{ print $1 $7 }' /etc/passwd 	Print first and seventh field of every line



# File Manipulation Utilities



##    sort

sort <filename> 	Sort the lines in the specified file, according to the characters at the beginning of each line.
cat file1 file2 | sort 	Combine the two files, then sort the lines and display the output on the terminal
sort -r <filename> 	Sort the lines in reverse order
sort -k 3 <filename> 	Sort the lines by the 3rd field on each line instead of the beginning

-u option, sort checks for unique values after sorting the records (lines)


##    uniq

uniq is used to remove duplicate lines in a text file and is useful for simplifying the text display.

sort file1 file2 | uniq > file3
sort -u file1 file2 > file3

To count the number of duplicate entries,
uniq -c filename 


##    paste

Suppose you have a file that contains the full name of all employees and another file that lists their phone numbers and Employee IDs. You want to create a new file that contains all the data listed in three columns: name, employee ID, and phone number. How can you do this effectively without investing too much time?

    -d delimiters, which specify a list of delimiters to be used instead of tabs for separating consecutive values on a single line. Each delimiter is used in turn; when the list has been exhausted, paste begins again at the first delimiter.
    -s, which causes paste to append the data in series rather than in parallel; that is, in a horizontal rather than vertical fashion.

'space', 'tab', '|', 'comma' are delimiters the syntax to use a different delimiter is as follows:

$ paste -d, file1 file2

##    join

The above task can be achieved using join, which is essentially an enhanced version of paste. It first checks whether the files share common fields, such as names or phone numbers, and then joins the lines in two files based on a common field.




##    split

split is used to break up (or split) a file into equal-sized segments for easier viewing and manipulation, and is generally used only on relatively large files


$ split american-english dictionary



## tr


The tr utility is used to translate specified characters into other characters or to delete them. The general syntax is as follows:

$ tr [options] set1 [set2]


$ tr abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ 	Convert lower case to upper case
$ cat city | tr a-z A-Z
$ tr '{}' '()' < inputfile > outputfile 			Translate braces into parenthesis
$ echo "This is for testing" | tr [:space:] '\t' 		Translate white-space to tabs
$ echo "This   is   for    testing" | tr -s [:space:]		Squeeze repetition of characters using -s
$ echo "the geek stuff" | tr -d 't' 				Delete specified characters using -d option
$ echo "my username is 432234" | tr -cd [:digit:] 		Complement the sets using -c option
$ tr -cd [:print:] < file.txt 					Remove all non-printable character from a file
$ tr -s '\n' ' ' < file.txt 					Join all the lines in a file into a single line



## tee

strings is used to extract all printable character strings found in the file or files given as arguments. It is useful in locating human-readable content embedded in binary files; for text files one can just use grep.

$ ls -l | tee newfile 

## wc 

$ wc -l filename

–l 	Displays the number of lines.
-c 	Displays the number of bytes.
-w 	Displays the number of words.


## cut 

cut is used for manipulating column-based files and is designed to extract specific columns. The default column separator is the tab character. A different delimiter can be given as a command option.
 
$ ls -l | cut -d" " -f3



































