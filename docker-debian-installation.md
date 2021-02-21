```bash
sudo apt-get remove docker docker-engine docker.io


sudo apt-get update

sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common \
     iputils-ping


curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -


sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install docker-ce


```

```bash
sudo groupadd sudo $USER


sudo groupadd docker
sudo usermod -aG docker $USER
sudo shutdown  -r now
```

```bash
sudo systemctl enable docker
```


# Use the OverlayFS storage driver



```bash
sudo systemctl stop docker
sudo cp -au /var/lib/docker /var/lib/docker.bk

sudo vi /etc/docker/daemon.json
```
```json
{
  "storage-driver": "overlay2"
}
```

```bash
sudo systemctl start docker
sudo docker info

# Storage Driver: overlay2
```




```bash
sudo pip install docker-compose
```
