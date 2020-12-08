# menu config


```
get_idf
cd project

idf.py menuconfig
```



1. increase FLASHSIZE

```
idf.py menuconfig

	serial flasher config
		flash size ({1,2,4,8,16}Mb)
```