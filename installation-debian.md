# installation in debian in docker


```bash
sudo apt-get install arp-scan

sudo apt-get install iputils-ping
sudo apt-get install vim-tiny
sudo apt-get install tree
sudo apt-get install mupdf mupdf-tools # for rails

sudo apt-get install mariadb-client default-mysql-client

sudo apt-get install libmagickwand-dev

sudo apt-get install libssl-dev libpq-dev postgresql-client-common

# php compilation
sudo apt-get install re2c libtidy-dev libxslt1-dev libxslt1-dev libzip-dev
```


# installation in workstation

adding user to sudoers

```bash
visudo
```


avoid duplicate lines in .bash_history
```
vi ~/.bashrc:
export HISTCONTROL=ignoreboth:erasedups
```



```
sudo su   #

sudo su - # this will load ~/.bash_profile as source by default.
```



mounting the existing second disk
```bash
lsblk

# NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
# sda      8:0    0 447.1G  0 disk
# ├─sda1   8:1    0 446.2G  0 part /
# ├─sda2   8:2    0     1K  0 part
# └─sda5   8:5    0   976M  0 part [SWAP]
# sdb      8:16   0   1.8T  0 disk
# └─sdb1   8:17   0   1.8T  0 part
# sr0     11:0    1  1024M  0 rom

sudo blkid

# /dev/sda1: UUID="f294c64a-2582-4f88-9c37-6e391c26ef09" TYPE="ext4" PARTUUID="a266daf8-01"
# /dev/sda5: UUID="e15c46bf-ed4f-493d-b118-db095d65db6a" TYPE="swap" PARTUUID="a266daf8-05"
# /dev/sdb1: UUID="307b216f-6e70-43a1-84eb-d919d22ea9ec" TYPE="ext4" PARTUUID="30fa50df-f4ef-4c98-9a59-db665b6d882b"
# /dev/sdc1: UUID="adcb26fe-987f-4973-adc8-f892277f7207" TYPE="ext4" PARTUUID="efc51912-01"
# /dev/sdc5: UUID="4d12888b-f544-459b-a49e-93a40d3b0bc1" TYPE="swap" PARTUUID="efc51912-05

# add config to /etc/fstab
sudo mkdir -p /media/storeHD

UUID=307b216f-6e70-43a1-84eb-d919d22ea9ec /media/storeHD ext4, auto,users,exec,rw, 1 0
```



```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
```


```
deb http://http.us.debian.org/debian jessie main contrib non-free

deb http://security.debian.org jessie/updates main contrib non-free
```

```
deb http://deb.debian.org/debian buster main
deb-src http://deb.debian.org/debian buster main

deb http://deb.debian.org/debian-security/ buster/updates main
deb-src http://deb.debian.org/debian-security/ buster/updates main

deb http://deb.debian.org/debian buster-updates main
deb-src http://deb.debian.org/debian buster-updates main


deb http://deb.debian.org/debian buster main contrib non-free
deb-src http://deb.debian.org/debian buster main contrib non-free

deb http://deb.debian.org/debian-security/ buster/updates main contrib non-free
deb-src http://deb.debian.org/debian-security/ buster/updates main contrib non-free

deb http://deb.debian.org/debian buster-updates main contrib non-free
deb-src http://deb.debian.org/debian buster-updates main contrib non-free


deb http://deb.debian.org/debian buster-backports main contrib non-free
deb-src http://deb.debian.org/debian buster-backports main contrib non-free
```




```bash
sudo apt install -y build-essential cmake g++ httpie




sudo apt-get install apt-transport-https zip htop tilix tmux iotop
apt install gvfs-backends gvfs-fuse
apt install  meld rsync gtypist alacarte graphviz openssl lsb-base lsb-release ffmpeg unrar-free nmap imagemagick bison p7zip-full



sudo apt-get install libffi6 libffi-dev libreadline7 libreadline-dev libssl-dev

sudo apt-get install redis-tools mariadb-client libmariadb-dev postgresql-client-common sqlite3 libsqlite3-dev libmongo-client-dev

# only psql


sudo apt-get update
```

# docker  & docker-compose


```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```
...



# c++ Installation

```bash
apt-get install g++ build-essential manpages-dev
```

# python

```bash
pip install awslogs --user

# into .bash_profile
# export PATH="$HOME/.local/bin:"
```







```
sudo apt-get update
vi /etc/apt/sources.list
sudo apt-get update
apt s gnome
apt
apt-cache search gnome 
apt-cache search tweak gnome-tweak-tool vlc
sudo apt install
sudo apt install snapd flatpak

sudo apt-cache search keepassxc
sudo apt-get install keepassxc
sudo apt-get install transmission calibre filezilla wine okular
history


atom install

```bash
wget -qO - https://packagecloud.io/AtomEditor/atom/gpgkey | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/AtomEditor/atom/any/ any main" > /etc/apt/sources.list.d/atom.list'
sudo apt-get update
sudo apt-get install atom
```



visual studio code
```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

sublime text

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install sublime-text sublime-merge
```


dbeaver.io

```bash
wget -O - https://dbeaver.io/debs/dbeaver.gpg.key | sudo apt-key add -
echo "deb https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list
sudo apt-get update && sudo apt-get install dbeaver-ce

```

sqlite studio

```

```






snap install

```bash
sudo apt-get snapd

sudo snap install skype --classic
sudo snap install slack --classic
sudo snap install postman


sudo snap install --classic heroku

```


chrome

```bash
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
deb http://dl.google.com/linux/chrome/deb/ stable main
sudo apt-get install google-chrome-stable
```


```bash
sudo apt-get install
```


sdkman install



zoom.us install


```bash
sudo apt install libglib2.0-0 libgstreamer-plugins-base0.10-0  libxcb-shape0 libxcb-shm0 libxcb-xfixes0 libxcb-randr0 libxcb-image0 libfontconfig1 libgl1-mesa-glx libxi6 libsm6 libxrender1 libpulse0 libxcomposite1 libxslt1.1 libsqlite3-0 libxcb-keysyms1 libxcb-xtest0

sudo apt install ./zoom_amd64.deb

sudo apt remove zoom
```


mongo shell

```bash
sudo apt-get install gnupg

wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -


echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/4.4 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

sudo apt-get update


# only mongo-org-shell
sudo apt-get install -y mongodb-org-shell
```


postgres client

```bash
apt-get install postgresql-client
```

mysql client

```bash
apt-get install default-mysql-client # buster
```




zoom

```
sudo apt install libglib2.0-0 libgstreamer-plugins-base0.10-0  libxcb-shape0 libxcb-shm0 libxcb-xfixes0 libxcb-randr0 libxcb-image0 libfontconfig1 libgl1-mesa-glx libxi6 libsm6 libxrender1 libpulse0 libxcomposite1 libxslt1.1 libsqlite3-0 libxcb-keysyms1 libxcb-xtest0 
```
