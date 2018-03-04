# bash from edx course


## Environment Variables

	$ env
	$ set	
	$ export



### setting environment variables


	$ echo $SHELL    
	$ export new variable
	$ export VARIABLE=value

	$ VARIABLE=value; export VARIABLE

	$ echo $PATH
	$ export PATH=$HOME/bin:$PATH


### add variable permanently


    Edit ~/.bashrc and add the line export VARIABLE=value
	$ source ~/.bashrc 


### The PS1 Variable and the Command Line Prompt

Prompt Statement (PS) is used to customize your prompt string in your terminal windows to display the information you want. PS1 is the primary prompt variable which controls what your command line prompt looks like. The following special characters can be included in PS1:

param    | mean
---------|-----
\u | User name
\h | Host name
\w | Current working directory
\! | History number of this command
\d | Date


### the history command


Several associated environment variables can be used to get information about the history file. 

VARIABLE        | use
----------------|-----
HISTFILE	 	| The location of the history file. 
HISTFILESIZE	| The maximum number of lines in the history file (default 500). 
HISTSIZE		| The maximum number of commands in the history file. 
HISTCONTROL		| How commands are stored. 
HISTIGNORE		| Which command lines can be unsaved.


### Finding and Using Previous Commands

moving throught history |  action
--------------------|-----
Up/Down arrow keys 	| 	Browse through the list of commands previously executed
!! 					| (Pronounced as bang-bang) 	Execute the previous command
CTRL-R 				| Search previously used commands
! 					| Start a history substitution
!$ 					| Refer to the last argument in a line
!n 					| Refer to the nth command line
!string 			| Refer to the most recent command starting with string










## switching quickly between directories

cd  /home/user/wathever/folder1
cd  /home/user/wathever/folder2
cd -
pwd /home/user/wathever/folder1

pushd       push dir at stack
popd        pop dir from stack

## wildcards

Wildcard 			Result
?  		    Matches any single character
* 		    Matches any string of characters
[set] 		Matches any character in the set of characters, for example [adf] will match any occurrence of "a", "d", or "f"
[!set] 		Matches any character not in the set of characters


## searching files with locate 

    updatedb
    locate text


## searching files with find

    find [path] -name pattern 	# search by pattern
    find [path] -iname pattern	# ignore pattern

    find [path] -type d pattern	# search only directories
    find [path] -type f pattern	# search only files

### searching by date
    
-ctime n File's status was last changed n*24 hours ago.

    find <path> -ctime <number-days>
    find / -ctime 3

-atime  You can also search for accessed/last read 
-mtime  modified/last written (-mtime) times.

in -cmin, -amin, and -mmin

### searching by size

    find / -size 0
    find / -size +10M -exec command {} ’;’







## searchin and execute command every file

can use of find is being able to run commands on the files that match your search criteria. The -exec option is used for this purpose.

    find -name "*.swp" -exec rm {} ’;’

The {} (squiggly brackets) is a place holder that will be filled with all the file names that result from the find expression, and the preceding command will be run on each one individually.

Please note that you have to end the command with either ‘;’ (including the single-quotes) or "\;". Both forms are fine.

    find -name "*.swp" -ok echo {} ’;’
    find -name "*.swp" -ok rm {} ’;’

-ok option, which behaves the same as -exec, except that find will prompt you for permission before executing the command. 



## man 

    man -k
    man -a

for browse by man page you can use  key n (next) | 	key p (previous) |	key u (up node)





## Introduction to Scripting

The #!/bin/bash in the first line should be recognized by anyone who has developed any kind of script in UNIX environments. listed at file /etc/shells

/usr/bin/perl, /bin/bash, /bin/csh, /usr/bin/python, /bin/sh

    #!/bin/bash
    # Interactive reading of a variable
    echo "ENTER YOUR NAME"
    read name
    # Display variable input
    echo The name given was :$name



All shell scripts generate a return value upon finishing execution, the value can be set with the exit statement. By convention, success is returned as 0, and failure is returned as a non-zero value.



Character       |	Description
----------------|-----------------------
# 		   		| Used to add a comment, except when used as \#, or as #! when starting a script
\ 		    	| Used at the end of a line to indicate continuation on to the next line
; 		    	| Used to interpret what follows as a new command to be executed next
&&		    	| Similar to ; but if you may want to abort subsequent commands when an earlier one fails If the first command fails, the second one will never be executed.
&#124;&#124;		    | you proceed until something succeeds and then you stop executing any further steps.
$ 		    	| Indicates what follows is an environment variable
> 		    	| Redirect output
>> 		    	| Append output
< 		   		| Redirect input
&#124; 		    	| Used to pipe the result into the next command






## Script Parameters

    ./script.sh /tmp
    ./script.sh 100 200

identifier | meanings
-----------|-------------
$0 		        | Script name
$1 		        | First parameter
$2, $3, etc. 	| Second, third parameter, etc.
$* 		        | All parameters
$# 		        | Number of arguments




## Command Substitution

you can get command substitution by:

- enclosing the inner command with backticks (`)
- By enclosing the inner command in $( )

example:

    $ ls /lib/modules/$(uname -r)/
    $ ls /lib/modules/´uname -r´/




## Environment Variables

You can get a list of environment variables with the env, set, or printenv commands. HOME, PATH, HOST are examples of environment variables.

    MYCOLOR=blue
    echo $MYCOLOR


By default, the variables created within a script are available only to the subsequent steps of that script. To make them available to child processes, they must be promoted to environment variables using the export statement, as in:

    export VAR=value

While child processes are allowed to modify the value of exported variables, the parent will not see any changes; exported variables are not shared, they are only copied and inherited.




##functions

    function_name () {
        command...
    }

the first argument can be referred to as $1, the second as $2, etc.


## control sentences

### The if Statement

sintax if statement at one line

	if TEST-COMMANDS; then CONSEQUENT-COMMANDS; fi

sintax if statement at multiples lines 

    if condition 
    then
        if condition
        then
            statements
        else
            statements
        fi
    elif
    then
        statements
    else
        statements
    fi

example

    file = $1
    if [ -f $file ]
    then
        echo -e "$file exist"
    else
        echo -e "$file does not exist"
    if


In modern scripts, you may see doubled brackets as in

	[[ -f /etc/passwd ]]. 
    
This is not an error. It is never wrong to do so and it avoids some subtle problems, such as referring to an empty environment variable without surrounding it in double quotes; we will not talk about this here.


#### conditionals to use at if

bash provides a set of file conditionals, that can used with the if statement, including:

conditional | meanings
------------|-
-e file 	|Checks if the file exists.
-d file 	|Checks if the file is a directory.
-f file 	|Checks if the file is a regular file (i.e., not a symbolic link, device node, directory, etc.)
-s file 	|Checks if the file is of non-zero size.
-g file 	|Checks if the file has sgid set.
-u file 	|Checks if the file has suid set.
-r file 	|Checks if the file is readable.
-w file 	|Checks if the file is writable.
-x file 	|Checks if the file is executable.

You can view the full list of file conditions using the command man 1 test

binary conditional |
&& 	AND 	The action will be performed only if both the conditions evaluate to true.
|| 	OR 	The action will be performed if any one of the conditions evaluate to true.
! 	NOT 	The action will be performed only if the condition evaluates to false. 



Numerical Tests | meanings
----------------|-
-eq 	| Equal to
-ne 	| Not equal to
-gt 	| Greater than
-lt 	| Less than
-ge 	| Greater than or equal to
-le 	| Less than or equal to

Example the operator -gt returns TRUE if number1 is greater than number2.
	
    [ $number1 -gt $number2 ]



String test | meanings
------------|------
-eq 	| Equal to
-ne 	| Not equal to
-gt 	| Greater than
-lt 	| Less than
-ge 	| Greater than or equal to
-le 	| Less than or equal to


    if [ $string1 == $string2 ] ; then echo "match" ; fi
    if [[ $STR1 = $STR2 ]] ; then echo match found ; fi 



#### Arithmetic Expressions

    echo $(expr 8 + 8) DEPRECATED
    $((...))
    echo $((x+1))
    let x=( 1 + 2 ); echo $x
    var=$((...)).



#### String manipulation

sintax  | manipulation
--------|------------
[[ string1 > string2 ]]		| Compares the sorting order of string1 and string2.
[[ string1 == string2 ]]	| Compares the characters in string1 with the characters in string2.
myLen1=${#string1}			| Saves the length of string1 in the variable myLen1.
${string:s:n}				| Extract the first n characters starting at s position of string 
${string#*.}				| To extract all characters in a string after a dot (.)


    myvar='string'
    chrlen=${#myvar}
    echo $chrlen


### The case Statement


    case expression in
       pattern1) execute commands;;
       pattern2) execute commands;;
       pattern3) execute commands;;
       pattern4) execute commands;;
       * )       execute some default commands or nothing ;;
    esac





### Looping Constructs for, while, until

for loop sintax 

    for variable-name in list
    do
        execute one iteration for each item in the list until the list is finished
    done

example:

    for j in 7 8 9 ; do echo $j ; done 

while loop sintax

    while condition is true
    do
        Commands for execution
        ----
    done

until loop sintax

    until condition is false
    do
        Commands for execution
        ----
    done






## Introduction to Script Debugging

You can run a bash script in debug mode either by doing bash –x 

./script_file,  or bracketing parts of the script with set -x and set +x. The debug mode helps identify the error because:

It traces and prefixes each command with the + character.
It displays each command before executing it.
It can debug only selected parts of a script (if desired) with:

    set -x    # turns on debugging
    ...
    set +x    # turns off debugging




### Redirecting Errors to File and Screen


    bash script.sh 2>error.txt



### Creating Temporary Files and Directories


TEMP=$(mktemp /tmp/tempfile.XXXXXXXX) 		To create a temporary file
TEMPDIR=$(mktemp -d /tmp/tempdir.XXXXXXXX) 	To create a temporary directory

The XXXXXXXX is replaced by the mktemp utility with random characters to ensure the name of the temporary file cannot be easily predicted and is only known within your program.


/dev/null bit bucket or black hole.

In the above command, the entire standard output stream is ignored, but any errors will still appear on the console. However, if one does

    $ ls -lR /tmp > /dev/null

both stdout and stderr will be dumped into /dev/null.
    
    $ ls -lR /tmp >& /dev/null


### Random Numbers and Data

entropy pool, The Linux kernel offers the /dev/random and /dev/urandom device nodes,























