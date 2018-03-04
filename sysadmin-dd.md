# dd - copy and convert file & in Unix all are a file...


    dd [params in] [params out]

|if=input path|
|of=output path|
|ibs=N| N bytes from input
|obs=N| N bytes from output
|bs=N| N bytes from input and N bytes from output

|skip=N | skip N blocks from input and size is specified at ibs
|seek=N | seek N blocks before write at output and size is specified at obs


       count_bytes
              treat 'count=N' as a byte count (iflag only)

       skip_bytes
              treat 'skip=N' as a byte count (iflag only)

       seek_bytes
              treat 'seek=N' as a byte count (oflag only)

conv=mode[,mode,...]

|cbs=N


dd if=somefile bs=4096 skip=1337 count=31337000 iflag=skip_bytes,count_bytes

In case you are using seek= as well, you may also consider oflag=seek_bytes.

From info dd:

`count_bytes'
      Interpret the `count=' operand as a byte count, rather than a
      block count, which allows specifying a length that is not a
      multiple of the I/O block size.  This flag can be used only
      with `iflag'.

`skip_bytes'
      Interpret the `skip=' operand as a byte count, rather than a
      block count, which allows specifying an offset that is not a
      multiple of the I/O block size.  This flag can be used only
      with `iflag'.

`seek_bytes'
      Interpret the `seek=' operand as a byte count, rather than a
      block count, which allows specifying an offset that is not a
      multiple of the I/O block size.  This flag can be used only
      with `oflag'.


# 
dd skip=31744 ibs=46587953664 if=sas.00.raw of=sas-00.ntfs


dd skip=62 count=90992097 if=sas.00.raw of=sas-00.ntfs



# kpartx

for mount images file of partitions on a /dev/loopXX

kpartx -a -v /tmp-mnt/BACKUP_final.img

for umount 

kpartx -dv drive.img


kpartx - Create device maps from partition tables

SYNOPSIS
       kpartx [-a | -d | -l] [-v] wholedisk

DESCRIPTION
       This  tool,  derived from util-linux' partx, reads partition tables on specified
       device and create device maps over partitions segments detected.  It  is  called
       from hotplug upon device maps creation and deletion.

OPTIONS
       -a     Add partition mappings

       -r     Read-only partition mappings

       -d     Delete partition mappings

       -u     Update partition mappings

       -l     List partition mappings that would be added -a

       -p     set device name-partition number delimiter

       -f     force creation of mappings; overrides 'no_partitions' feature

       -g     force GUID partition table (GPT)

       -v     Operate verbosely

       -s     Sync mode. Don't return until the partitions are created


To mount all the partitions in a raw disk image:

      kpartx -av disk.img

This will output lines such as:

      loop3p1 : 0 20964762 /dev/loop3 63

The  loop3p1 is the name of a device file under /dev/mapper which you can use to
access the partition, for example to fsck it:

      fsck /dev/mapper/loop3p1

When you're done, you need to remove the devices:

      kpartx -d disk.img

# dd with progress using pv (pipe viewer)

      dd if=/dev/urandom | pv | dd of=/dev/null
      dd if=/dev/urandom of=/dev/null status=progress


# ddrescue


# dcfldd 

dcfldd is a fork of dd that is an enhanced version developed by Nick Harbour, who at the time was working for the United States' Department of Defense Computer Forensics Lab.[17][18][19] Compared to dd, dcfldd allows for more than one output file, supports simultaneous multiple checksum calculations, provides a verification mode for file matching, and can display the percentage progress of an operation.






