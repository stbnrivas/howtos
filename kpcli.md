# kpcli command line
A command line interface (interactive shell) to work with KeePass 1.x or 2.x database files.
This program was inspired by my use of the CLI of the Ked Password Manager ("kedpm -c") combined with my need to migrate to KeePass.


```
Usage: kpcli [--kdb=<file.kdb>] [--key=<file.key>]

  --kdb         Optional KeePass database file to open (must exist).
  --key         Optional KeePass key file (must exist).
  --pwfiles     Read master password from file instead of console.
  --histfile    Specify your history file (or perhaps /dev/null).
  --readonly    Run in read-only mode; no changes will be allowed.
  --timeout=i   Lock interface after i seconds of inactivity.
  --command     Run single command and exit (no interactive session).
  --no-recycle  Don't store entry changes in /Backup or "/Recycle Bin".
  --help        This message.
```



```bash
kpcli --kdb ~/file.kdbx
kpcli --kdb ~/file.kdbx --readonly

find $key

# copy password
xp
# copy user
xu
# copy url
xw
# clear
xx

quit
```
