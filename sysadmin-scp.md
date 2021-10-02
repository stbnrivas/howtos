# scp


 to easier the command modify `~/.ssh/config`

```bash
# personal
Host remote_host.es
Hostname XXX.XXX.XXX.XXX
PreferredAuthentications publickey
IdentitiesOnly yes
IdentityFile ~/.ssh/id_rsa
User your_user
Port your_port
```



- from remote to local

```bash
# r is recursive like copy a folder
scp -r $remote_server:$remote_fullpath_file $local_fullpath_file
```



- from local to remote

```bash
scp -r $local_fullpath_file  $username@$domain:$remote_full_path_file


scp -r backup.sql domain.es:/home/user/2021-06-05-backup.sql
```