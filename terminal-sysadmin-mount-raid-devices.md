# raid management device 


In particular NEVER NEVER NEVER use "mdadm --create" on an already-existing array unless you are being guided by an expert. It is the single most effective way of turning a simple recovery exercise into a major forensic problem - it may not be quite as effective as "dd if=/dev/random of=/dev/sda", but it's pretty close ... 

  fdisk -l
  blkid
  cat /proc/mdstat

  mdadm --stop /dev/md12*

  rpm -ql mdadm | grep "mdadm.conf"
  /usr/share/doc/mdadm-2.6.9/mdadm.conf-example
  /usr/share/man/man5/mdadm.conf.5.gz$ rpm -ql mdadm | grep "mdadm.conf"
  /usr/share/doc/mdadm-2.6.9/mdadm.conf-example
  /usr/share/man/man5/mdadm.conf.5.gz

  mdadm --verbose --detail --scan

## dd

use dd to get raw images of disk to work... like

  dd if=/dev/sdOri of=/dev/sdDest status=progress
  dd if=/dev/sgOri of=/dev/sgDest status=progress

## kpartx 

Create device maps from partition tables, This  tool,  derived from util-linux' partx, reads partition tables on specified device and create device maps over partitions segments detected.  It  is  called from hotplug upon device maps creation and deletion.

To mount all the partitions in a raw disk image:

  kpartx -av disk.img

This will output lines such as:

  loop3p1 : 0 20964762 /dev/loop3 63

## lsblk

check whereis mount with 

  lsblk

## gdisk

gdisk Interactive GUID partition table (GPT) manipulator

## fdisk

fdisk is a dialog-driven program for creation and manipulation of partition tables.  It under‐stands GPT, MBR, Sun, SGI and BSD partition tables.


##losetup

set up and control loop devices


  dd if=/dev/zero of=~/file.img bs=1MiB count=10
  losetup --find --show ~/file.img
  /dev/loop0
  mkfs -t ext2 /dev/loop0
  mount /dev/loop0 /mnt
  ...
  umount /dev/loop0
  losetup --detach /dev/loop0







## mdadm

mdadm is used for building, managing, and monitoring Linux md devices (aka RAID arrays)

  mdadm --create device options...
      Create a new array from unused devices.
  mdadm --assemble device options...
      Assemble a previously created array.
  mdadm --build device options...
      Create or assemble an array without metadata.
  mdadm --manage device options...
      make changes to an existing array.
  mdadm --misc options... devices
      report on or modify various md related devices.
  mdadm --grow options device
      resize/reshape an active array
  mdadm --incremental device
      add/remove a device to/from an array as appropriate
  mdadm --monitor options...
      Monitor one or more array for significant changes.
  mdadm device options...
      Shorthand for --manage.

Any parameter that does not start with '-' is treated as a device name
or, for --examine-bitmap, a file name.
The first such name is often the name of an md device.  Subsequent
names are often names of component devices


  mdadm --verbose --detail --scan
  mdadm --verbose --detail --scan > /etc/mdadm.conf

  cat /etc/mdadm.conf

  mdadm --assemble --scan --verbose
  mdadm --stop /dev/md123
  mdadm --stop /dev/md124
  mdadm --stop /dev/md125
  mdadm --stop /dev/md126
  mdadm --stop /dev/md127

  mdadm --assemble --scan --verbose
  cat /proc/mdstat
  mount /dev/md126 /root/raid
  ls /root/raid/
  df -h

### umount

  umount /dev/mdX

### verifying status of RAID arrays

  cat /proc/mdstat
  mdadm --detail /dev/md0

### stop array

  mdadm -S /dev/mdX
  mdadm --stop /dev/mdX

### reassemble volume

  mdadm --assemble /dev/md0 /dev/sda3

### to remove disk because it is fail
  
  mdadm --fail /dev/md0 /dev/sda1
  mdadm --remove /dev/md0 /dev/sda1

### add a disk to an existing array
  
  mdadm --add /dev/md0 /dev/sdb1







## raid problem


mdadm --auto-detect

partx -av /media/storeHD/sas-00.raw
partx -av /media/storeHD/sas-01.raw
partx -av /media/storeHD/sas-02.raw

lsblk
  loop1       7:1    0  68.4G  0 loop 
  loop2       7:2    0  68.4G  0 loop 
  loop0       7:0    0  68.4G  0 loop 
  └─loop0p1 253:0    0  43.4G  0 part 

mdadm --examine /dev/loop0
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  /dev/loop0:
    MBR Magic : aa55
  Partition[0] :     90992097 sectors at           63 (type 07)
  Partition[1] :    195286140 sectors at     90992160 (type 07)

mdadm --examine /dev/loop1
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: No md superblock detected on /dev/loop1.

mdadm --examine /dev/loop2
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: Unknown keyword INACTIVE-ARRAY
  mdadm: No md superblock detected on /dev/loop2.


mdadm --assemble /dev/sdc /dev/loop[012]
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Cannot assemble mbr metadata on /dev/loop0
mdadm: /dev/loop0 has no superblock - assembly aborted





mdadm --assemble --scan

mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1
mdadm --assemble /dev/sdb /dev/sd[cd]1

mdadm --create /dev/md0 --chunk=4 --level=0 --raid-devices=2 /dev/sda1 /dev/sdb1
mdadm --create /dev/md0 --level=5 --raid-devices=3 --spare-devices=0 /dev/sd[bcd]


###########################################################


another example

kpartx -f -r -a /media/storeHD/sas-00.raw.ori
kpartx -f -r -a /media/storeHD/sas-01.raw.ori
kpartx -f -r -a /media/storeHD/sas-02.raw.ori


losetup --list

mdadm --detail --scan >> /etc/mdadm.conf

mdadm --assemble --scan --detail --verbose --metadata=[ddf|imsm]




mdadm --examine /dev/loop0 /dev/loop1 /dev/loop2
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
/dev/loop0:
   MBR Magic : aa55
Partition[0] :     90992097 sectors at           63 (type 07)
Partition[1] :    195286140 sectors at     90992160 (type 07)
mdadm: No md superblock detected on /dev/loop1.
mdadm: No md superblock detected on /dev/loop2.



  mdadm --build md-device --chunk=X --level=Y --raid-devices=Z devices
  mdadm --create /dev/md0 --assume-clean --level=5 --verbose --raid-devices=4 /dev/loop0p1 /dev/loop1p1 /dev/loop2p1 /dev/loop3p
  mdadm --create /dev/md0 --metadata=ddf --level=5 --raid-devices=3 /dev/loop0p1 /dev/loop1 /dev/loop2


  --chunk=256
  --metadata=ddf
  --metadata=imsm





------------------------------------

## qnap nas 

  [~] # cat /proc/mdstat 
  Personalities : [linear] [raid0] [raid1] [raid10] [raid6] [raid5] [raid4] [multipath] 
  md3 : active raid1 sdd3[0]
        2920311616 blocks super 1.0 [1/1] [U]
        
  md2 : active raid1 sdc3[0]
        1943559616 blocks super 1.0 [1/1] [U]
        
  md1 : active raid1 sdb3[0] sda3[1]
        2920311616 blocks super 1.0 [2/2] [UU]
        
  md256 : active raid1 sdd2[3](S) sdc2[2](S) sdb2[1] sda2[0]
        530112 blocks super 1.0 [2/2] [UU]
        bitmap: 0/1 pages [0KB], 65536KB chunk

  md13 : active raid1 sdb4[0] sdd4[25] sdc4[24] sda4[1]
        458880 blocks super 1.0 [24/4] [UUUU____________________]
        bitmap: 1/1 pages [4KB], 65536KB chunk

  md9 : active raid1 sdb1[0] sdd1[25] sdc1[24] sda1[1]
        530048 blocks super 1.0 [24/4] [UUUU____________________]
        bitmap: 1/1 pages [4KB], 65536KB chunk

  unused devices: <none>

another info

  [~] # df -h
  Filesystem                Size      Used Available Use% Mounted on
  none                    250.0M    186.1M     63.9M  74% /
  devtmpfs                  3.8G      4.0K      3.8G   0% /dev
  tmpfs                    64.0M    356.0K     63.7M   1% /tmp
  tmpfs                     3.9G     24.0K      3.9G   0% /dev/shm
  tmpfs                    16.0M         0     16.0M   0% /share
  tmpfs                    16.0M         0     16.0M   0% /share/snapshot/export
  /dev/md9                493.5M    118.1M    375.4M  24% /mnt/HDA_ROOT
  cgroup_root               3.9G         0      3.9G   0% /sys/fs/cgroup
  /dev/mapper/cachedev1
                            2.6T    512.3G      2.1T  19% /share/CACHEDEV1_DATA
  /dev/mapper/cachedev2
                            1.8T    929.8G    875.7G  51% /share/CACHEDEV2_DATA
  /dev/mapper/cachedev3
                            2.6T      1.9T    787.3G  71% /share/CACHEDEV3_DATA
  /dev/md13               355.0M    330.3M     24.7M  93% /mnt/ext
  tmpfs                    16.0M     36.0K     16.0M   0% /share/CACHEDEV1_DATA/.samba/lock/msg.lock
  tmpfs                    16.0M         0     16.0M   0% /mnt/ext/opt/samba/private/msg.sock
  tmpfs                     1.0M         0      1.0M   0% /mnt/rf/nd
  /dev/mapper/cachedev1
                            2.6T    512.3G      2.1T  19% /lib/modules/4.2.8/container-station
  /dev/mapper/cachedev1
                            2.6T    512.3G      2.1T  19% /share/CACHEDEV1_DATA/.qpkg/container-station/system-docker/devicemapper
