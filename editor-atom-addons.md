# Atom


## customization

edit -> preferences:


## create shortcut

ctr + shift + p > Settings -> Keybindings >

## addons

* file-icons
* language-docker
* trailing-spaces
* emmet
* language-procfile
* atom-beautify

* markdown-preview
* geojson-preview

* rainbow-csv

* path-copy
```
use ctrl + shift + c  to copy full path to current file

 Settings/Preferences ➔ Packages ➔ Search for
```

## shortcuts

+ CTRL + P (open document into project)
+ CTRL + SHIFT + M (markdown-prefiew)


## fixes

fix problem delete files of folder

+ first option

```bash
vi ~/.bash_profile
```

```bash
ELECTRON_TRASH=gio
```



+ second option

```bash
vi /usr/bin/gvfs-trash
```

```bash
#!/bin/bash
# GVFS updated and dropped gvfs-trash to gio, but Atom didn't update.
/usr/bin/gio trash "$@"
```







## show invisibles & show indent guide



