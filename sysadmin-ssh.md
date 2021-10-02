# ssh (secure shell)

## generate key without prompting

```bash
ssh-keygen -q -t rsa -N '' <<< ""$'\n'"y" 2>&1 >/dev/null

```



## configuration


Sometimes, while trying to connect to remote systems via SSH, you may encounter the error:
"Received disconnect from x.x.x.x port 22:2: Too many authentication failures"

```bash
# ~/.ssh/config
Host *
 IdentitiesOnly=yes
```



## key creation

```bash
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

xclip -sel clip < key.pub
```

## copy

```bash
ssh-copy-id -i ~/.ssh/mykey user@host

# or

touch ~/.ssh/authorized_keys
```

## fixing permissions after copy

```bash
chmod 600 ~/.ssh/id_rsa
```


## connection

```bash
ssh -p 333 user@server.com

ssh -p 333 -i ~/.ssh/key user@server.com
```


## ssh specifying identity file key

```bash
ssh -i ~/.ssh/id_rsa user@server.com
```


## ssh with automatic mapping between ssh key and domain


```bash
vi ~/.ssh/config
```

Add both host names and their identity file as follows:
```
Host server1.com
  IdentityFile ~/.ssh/id_dsa_server1
Host server2.com
  IdentityFile ~/.ssh/id_dsa_server2
```

## ssh with AWS

```bash
ssh -i id_key.pem admin@ec2-XXX-XXX-XXX-XXX.eu-west-1.compute.amazonaws.com
# Received disconnect from $IP port 22:2: Too many authentication failures
ssh -i id_key.pem -o IdentitiesOnly=yes admin@ec2-XXX-XXX-XXX-XXX.eu-west-1.compute.amazonaws.com

ssh -i ~/.ssh/key-eu-west-1.pem -o IdentitiesOnly=yes admin@ec2-XXX-XXX-XXX-XXX.eu-west-1.compute.amazonaws.com
```

## ssh over qnap

ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no admin@nasqnap.com

## Problem when migrate .ssh folder

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/config
chmod 600 ~/.ssh/id_rsa ~/.ssh/id_rsa.pub

chown $USER ~/.ssh/config
```


## list keys availables to agent-ssh

```bash
# check if agent is running
eval "$(ssh-agent -s)"

# list all your private keys
ssh-add -l
# list all your public keys
ssh-add -L
```






## add ssh key to authorized keys

```bash
mkdir -p ~/.ssh/

# To overwrite authorized_keys
cat your_key > ~/.ssh/authorized_keys

# To append to the end of authorized_keys
cat your_key >> ~/.ssh/authorized_keys
```




## debugging a ssh connection error

```bash
ssh -vvv user@server:port

```



### ERROR

`debug1: send_pubkey_test: no mutual signature algorithm`

fail to login with rsa key

```bash
sudo vim /etc/ssh/ssh_config

# add to the end of file:

PubkeyAcceptedKeyTypes +ssh-rsa
```
