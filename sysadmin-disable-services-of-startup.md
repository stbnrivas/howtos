# Runlevel

Runlevel is a mode of operation in the computer operating systems that implement Unix System V-style initialization. linux standard base defines:

LSB 4.1.0

ID 	| Name 	| Description
----|------|----
0 	| Halt 	Shuts down the system.
1 	| Single-user mode 	Mode for administrative tasks.[2][b]
2 	| Multi-user mode 	Does not configure network interfaces and does not export networks services.[c]
3 	| Multi-user mode with networking 	Starts the system normally.[1]
4 	| Not used/user-definable 	For special purposes.
5 	| Start the system normally with appropriate display manager (with GUI) 	Same as runlevel 3 + display manager.
6 	| Reboot 	Reboots the system.


In the past you can choose what service run at specific runlevel with chkconfig --list but now you must use  systmctl because sysVinit was replaced systemd

## list services 

	systemctl list-units --type=target
	systemctl enable <servicename>.service
	systemctl disable <servicename>.service
	systemctl start <servicename>.service
	systemctl stop <servicename>.service
	systemctl status <servicename>.service

runlevel command still works with systemd. You can continue using that however runlevels is a legacy concept in systemd and is emulated via ‘targets’ and multiple targets can be active at the same time. So the equivalent in systemd terms is

	systemctl list-units --type=target