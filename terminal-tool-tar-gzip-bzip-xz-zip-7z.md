# tar

```bash

# package multiples files into tar
tar -cvf my_files.tar file1 file2
```


# gzip

gzip is the most often used Linux compression utility. It compresses very well and is very fast. The following table provides some usage examples:ç

gzip * 				Compresses all files in the current directory; each file is compressed and renamed with a .gz extension.
gzip -r projectX 		Compresses all files in the projectX directory, along with all files in all of the directories under projectX.
gunzip foo 			De-compresses foo found in the file foo.gz. Under the hood, the gunzip command is actually the same as gzip –d.



# bzip2

bzip2 has a syntax that is similar to gzip but it uses a different compression algorithm and produces significantly smaller files, at the price of taking a longer time to do its work. Thus, it is more likely to be used to compress larger files.

bzip2 * 			Compresses all of the files in the current directory and replaces each file with a file renamed with a .bz2 extension.
bunzip2 *.bz2 			Decompresses all of the files with an extension of .bz2 in the current directory. Under the hood, bunzip2 is the same as calling bzip2 -d.


# xz

xz is the most space efficient compression utility used in Linux and is now used by www.kernel.org to store archives of the Linux kernel. Once again, it trades a slower compression speed for an even higher compression ratio


xz * 					Compresses all of the files in the current directory and replaces each file with one with a .xz extension.
xz foo 					Compresses the file foo into foo.xz using the default compression level (-6), and removes foo if compression succeeds.
xz -dk bar.xz 				Decompresses bar.xz into bar and does not remove bar.xz even if decompression is successful.
xz -dcf a.txt b.txt.xz > abcd.txt 	Decompresses a mix of compressed and uncompressed files to standard output, using a single command.
$ xz -d *.xz 				Decompresses the files compressed using xz.


# zip

zip backup * 		Compresses all files in the current directory and places them in the file backup.zip.
zip -r backup.zip ~ 	Archives your login directory (~) and all files and directories under it in the file backup.zip.
unzip backup.zip 	Extracts all files in the file backup.zip and places them in the current directory.


# archiving using tar

$ tar cvf dst.tar src-file-or-folder
$ tar xvf mydir.tar 		Extract all the files in mydir.tar into the mydir directory
$ tar zcvf mydir.tar.gz mydir 	Create the archive and compress with gzip
$ tar jcvf mydir.tar.bz2 mydir 	Create the archive and compress with bz2
$ tar Jcvf mydir.tar.xz mydir 	Create the archive and compress with xz
$ tar xvf mydir.tar.gz 		Extract all the files in mydir.tar.gz into the mydir directory. Note you do not have to tell tar it is in gzip format.
