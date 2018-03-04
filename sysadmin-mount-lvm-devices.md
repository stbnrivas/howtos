# How to mount an LVM partition on Linux

fails when

		mount /dev/sdcX /folder-destination
		mount: unknown filesystem type 'LVM2_member'
		sudo pvs

check VG colum, that show volume group

		lvdisplay <volume-group>

check LV name

		[root@server ~]# lvdisplay fedora
		--- Logical volume ---
		LV Path                /dev/fedora/swap
		LV Name                swap
		VG Name                fedora
		LV UUID                i4lVWf-9XiX-iJ20-Tr37-3glz-x4tO-sOcv2v
		LV Write Access        read/write
		LV Creation host, time localhost, 2015-03-07 12:35:37 +0100
		LV Status              available
		# open                 0
		LV Size                3.88 GiB
		Current LE             992
		Segments               1
		Allocation             inherit
		Read ahead sectors     auto
		- currently set to     256
		Block device           253:0

		--- Logical volume ---
		LV Path                /dev/fedora/home
		LV Name                home
		VG Name                fedora
		LV UUID                3eINJu-f6AU-npic-qSDI-afuO-xj4M-uvgf8Y
		LV Write Access        read/write
		LV Creation host, time localhost, 2015-03-07 12:35:37 +0100
		LV Status              available
		# open                 0
		LV Size                57.36 GiB
		Current LE             14684
		Segments               1
		Allocation             inherit
		Read ahead sectors     auto
		- currently set to     256
		Block device           253:1

		--- Logical volume ---
		LV Path                /dev/fedora/root
		LV Name                root
		VG Name                fedora
		LV UUID                pYi73v-Hw8H-4zWS-T80U-Ni0X-p5nQ-RItw18
		LV Write Access        read/write
		LV Creation host, time localhost, 2015-03-07 12:35:52 +0100
		LV Status              available
		# open                 0
		LV Size                50.00 GiB
		Current LE             12800
		Segments               1
		Allocation             inherit
		Read ahead sectors     auto
		- currently set to     256
		Block device           253:2

mount logical volume of volume group

		mount /dev/<volume-group>/<logical-volume> /mnt/folder-destination

examples:

		mount /dev/fedora/root /mnt/other-root
		mount /dev/fedora/home /mnt/other-home





