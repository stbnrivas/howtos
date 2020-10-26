# centos 7 system installation

## add extra packages (EPEL extra packages for Enterprise linux)

yum install epel-release dnf
yum install dnf
dnf install net-tools

## network tools

ifcfg
nmtui 
ip addr show

$ /sbin/ip addr show
$ /sbin/ip route show



systemctl start mysqld.service
systemctl enable mysqld.service

service <option> | --status-all | [ service_name [ command | --full-restart ] ]





# Fedora


## change history size at bash

```
vi ~/.bashrc

echo 'HISTSIZE=100000' >> ~/.bashrc && echo 'HISTFILESIZE=20000' >> ~/.bashrc

export HISTCONTROL=ignoreboth:erasedups
```


## packages packages...

dnf groupinstall "Development Tools"

dnf install lsb nmap openssh-client libcrypto git git-cola wget sqlite sqlite-devel sqlite-libs openssl-libs


dnf install gstreamer-plugins-bad gstreamer-plugins-ugly libaacs sox sox-plugins-* faad2 faad2-libs
lame lame-libs lame-devel libmad libmad-devel ffmpeg-devel ffmpeg

dnf install ffmpeg ffmpeg-devel ffmpegp-libs ffmpeg2theora youtube-dl

dnf install git git-cola cmake make gcc gcc-c++ perl python3 bash zlib-devel flex bison m4 coreutils autoconf automake libtool ncurses-devel wget bc doxygen graphviz upx pkg-config

dnf install rpmdevtools autoconf automake bison ImageMagick-devel

dnf install alacarte gnome-tweak-tool gvfs-smb picard vlc filezilla clementine p7zip p7zip-plugins unrar libunrar gparted clementine dropbox youtube-dl zathura zathura-plugins-all zathura-devel vlc 
gnome-terminal-nautilus transmission samba gvfs-samba gnome-font-viewer hamster-time-tracker bleachbit

dnf install libreoffice libreoffice-langpack-en hunspell-en aspell-en

dnf install ruby ruby-devel ruby-irb ruby-libs rubygems

dnf install -y gtypist meld

### search rpm

-skype

dnf install glibc.i686 libstdc++.i686 libXv.i686 qtwebkit.i686 libXScrnSaver.i686 alsa-plugins-pulseaudio.i686
rpm -Uhv skype-4.3.0.37-fedora.i586.rpm

-teamviewer




### howto check hw 3d acceleration

	glxinfo -i | grep render
	glxinfo -i | grep direct
	glxinfo -i | grep openGL
	glxgears -info
	xvinfo



### managing services old and new way

	/etc/init.d/mysqld start ## use restart after update
	service mysqld start ## use restart after update


	chkconfig --levels 235 mysqld on

	service mysqld status
	service mysqld start
	service mysqld stop


	/etc/init.d/httpd start ## use restart after update
	service httpd start ## use restart after update

	chkconfig --levels 235 httpd on
	systemctl enable httpd.service


dnf install install php-pecl-apc php-cli php-pear php-pdo php-mysql php-pgsql php-pecl-mongo php-sqlite php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml




