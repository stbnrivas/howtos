```bash
$ gsettings get org.freedesktop.Tracker.Miner.Files enable-monitors
true

$ gsettings get org.freedesktop.Tracker.Miner.Files ignored-files
['*~', '*.o', '*.la', '*.lo', '*.loT', '*.in', '*.csproj', '*.m4', '*.rej', '*.gmo', '*.orig', '*.pc', '*.omf', '*.aux', '*.tmp', '*.vmdk', '*.vm*', '*.nvram', '*.part', '*.rcore', '*.lzo', 'autom4te', 'conftest', 'confstat', 'Makefile', 'SCCS', 'ltmain.sh', 'libtool', 'config.status', 'confdefs.h', 'configure', '#*#', '~$*.doc?', '~$*.dot?', '~$*.xls?', '~$*.xlt?', '~$*.xlam', '~$*.ppt?', '~$*.pot?', '~$*.ppam', '~$*.ppsm', '~$*.ppsx', '~$*.vsd?', '~$*.vss?', '~$*.vst?', '*.desktop', '*.directory']
$ gsettings get org.freedesktop.Tracker.Miner.Files crawling-interval
-1
```



```bash
gsettings set org.freedesktop.Tracker.Miner.Files enable-monitors false
gsettings set org.freedesktop.Tracker.Miner.Files ignored-files "['*']"
gsettings set org.freedesktop.Tracker.Miner.Files crawling-interval -2

pkill tracker

rm -rf ~/.cache/tracker
```