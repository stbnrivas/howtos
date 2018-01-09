# raid management device 


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
