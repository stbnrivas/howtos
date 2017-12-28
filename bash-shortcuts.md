# bash shortcuts

CTRL-A  go to begin			go to end			CTRL-E
 ALT-B  move cursor back 1 word		move cursor forward 1 word	ALT-F
CTRL-W  delete one word backward	delete 1 word forward		ALT-D
CTRL-U  go to begin			delete all fforward		CTRL-K

CTRL-L  clean screen
CTRL-U  clean command typed
CTRL-R  reverse search

CTRL-SHIFT-V  paste text from the clipboard
CTRL-Y

## move previous directory
cd /../../folder1
cd -


## repeat your last command
!!


## keep executing a command until it succeeds
while ! ./run.sh do sleep 1; done


## view progress of file transfer
pv access.log | gzip > access.log.gz


# direct schedule events
echo wget https://example.com/test | at 2:00 PM


# display at output as a table
cat /etc/passwd | column -t


# copy with another name
	sample.txt
cp /home/sample.txt{,-old} 
	sample.txt
	sample.txt-old


# rename files with 
rename -v jpg jpeg ./*

