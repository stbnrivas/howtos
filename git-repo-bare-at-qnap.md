# create a bare repo at qnap

- create a folder into nas

```bash
/share/CACHEDEV1_DATA/Backups/repos/
```
- create a local repo
```bash
git init --bare
git clone --bare $source $destination
```
- clone repo into nas
```bash
scp -r $source $destination
scp -r $source admin@qnap_ip:/share/CACHEDEV1_DATA/Development/repos/
```
- add remote into local repo
```bash
git add remote add nastt ssh://admin@qnap_ip:/share/CACHEDEV1_DATA/Development/repos/project
```