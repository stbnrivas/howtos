# Atom


## customization

edit -> preferences:

## addons

* file-icons
* language-docker
* trailing-spaces
* emmet


* markdown-preview
* geojson-preview

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


