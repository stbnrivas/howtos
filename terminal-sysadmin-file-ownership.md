# file ownership commands chown chgrp chmod

- chown 	Used to change user ownership of a file or directory
- chgrp 	Used to change group ownership
- chmod 	Used to change the permissions on the file, which can be done separately for owner, group and the rest of the world (often named as other.)


## chmod

	ls -l somefile
	-rw-rw-r-- 1 coop coop 1601 Mar 9 15:04 somefile


rwx: rwx: rwx
 u:   g:   o

mask | mean
-----|--
7 	| means read/write/execute
6 	| means read/write
5 	| means read/execute.
4 	| if read permission is desired.
2 	| if write permission is desired.
1 	| if execute permission is desired.

	$ chmod 751 file.sh
	$ chmod +r arch.txt
	$ chmod u=rw,go= arch.txt

## chown

	$ chown user:group file


## chgrp

	chgroup group file


