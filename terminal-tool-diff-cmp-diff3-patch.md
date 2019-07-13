# diff for text files

  $ diff path path

| -c	| Provides a listing of differences that include 3 lines of context before and after the lines differing in content |
| -r 	|Used to recursively compare subdirectories, as well as the current directory|
| -i 	| Ignore the case of letters|
| -w 	| Ignore differences in spaces and tabs (white space)|
| -q 	| Be quiet: only report if files are different without listing the differences|


# cmp for binary files

  cmp

| -b |  --print-bytes                 print differing bytes |
| -i |  --ignore-initial=SKIP         skip first SKIP bytes of both inputs |
| -i |  --ignore-initial=SKIP1:SKIP2  skip first SKIP1 bytes of FILE1 and |
|    |                                first SKIP2 bytes of FILE2 |
| -l |  --verbose                     output byte numbers and differing byte values |
| -n |  --bytes=LIMIT                 compare at most LIMIT bytes |
| -s |  --quiet, --silent             suppress all normal output |
|    |  --help                        display this help and exit |
| -v |  --version                     output version information and exit |


# using diff3 and patch

You can compare three files at once using diff3, which uses one file as the reference basis for the other two.

  $ diff3 MY-FILE COMMON-FILE YOUR-FILE

meld is a good gui tool for diff3

# patch 

A patch file contains the deltas (changes) required to update an older version of a file to the new one. The patch files are actually produced by running diff with the correct options, as in:

  $ diff -Nur originalfile newfile > patchfile

To apply a patch, you can just do either of the two methods below:

  $ patch -p1 < patchfile
  $ patch originalfile patchfile

## using diff and patch

According to the man page for patch, the preferred options for preparing a patch with

$ diff -Naur path path

-a treat all files as text

