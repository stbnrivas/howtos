## mounting a qnap static simple volume


before check the partitions of the device 

```bash
ls /dev/sdc
# sdc   sdc1  sdc2  sdc3  sdc4  sdc5 
```


let's try with linear 
```bash
# sintax: mdadm [mode] <raiddevice> [options] <component-devices>
mdadm \
	--assemble /dev/md0 \
	--level=linear /dev/sdc3
```
	option --level not valid in assemble mode


# mdadm --assemble /dev/md0 /dev/sdc3
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: /dev/md0 has been started with 1 drive.


mount /dev/md0 /root/disk1
mount: /root/disk1: unknown filesystem type 'drbd'.



mdadm --verbose --detail --scan /dev/md0 
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
mdadm: Unknown keyword INACTIVE-ARRAY
ARRAY /dev/md0 level=raid1 num-devices=1 metadata=1.0 name=2 UUID=bf145006:50f7f29c:de6dc4d8:14229ce1
   devices=/dev/sdc3
   

# mount -t ext4 /dev/md0 /root/disk1
mount: /root/disk1: wrong fs type, bad option, bad superblock on /dev/md0, missing codepage or helper program, or other error.


# vgscan --cache
  Reading volume groups from cache.
  Found volume group "vg288" using metadata type lvm2

AWARD!!!


# vgchange -ay vg288
  2 logical volume(s) in volume group "vg288" now active

AWARD AGAIN!!!

# lvs
  LV    VG    Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  lv2   vg288 -wi-a-----  1.79t                                                    
  lv545 vg288 -wi-a----- 18.54g 
  
  
# lsblk 
NAME              MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
...
sdc                 8:32   0   1.8T  0 disk  
├─sdc1              8:33   0 517.7M  0 part  
├─sdc2              8:34   0 517.7M  0 part  
├─sdc3              8:35   0   1.8T  0 part  
│ └─md0             9:0    0   1.8T  0 raid1 
│   ├─vg288-lv545 253:0    0  18.5G  0 lvm   
│   └─vg288-lv2   253:1    0   1.8T  0 lvm   
├─sdc4              8:36   0 517.7M  0 part  
└─sdc5              8:37   0     8G  0 part  
sr0                11:0    1  1024M  0 rom 

# ls /dev/vg288/lv* -l
lrwxrwxrwx. 1 root root 7 Mar 28 21:09 /dev/vg288/lv2 -> ../dm-1
lrwxrwxrwx. 1 root root 7 Mar 28 21:09 /dev/vg288/lv545 -> ../dm-0


$ sudo mount /dev/vg288/lv2 ./hdwork
$ cd hdwork/
$ ls
aquota.user  lost+found  syncthing-folder  mypreciousfolder  work


