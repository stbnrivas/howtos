# pyenv installation

requeriments

```bash
sudo apt install bzip2



sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev


sudo apt purge -y python2.7-minimal
```




```bash


git clone https://github.com/pyenv/pyenv.git ~/.pyenv

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile


# old
# echo 'eval "$(pyenv init -)"' >> ~/.bash_profile

# new
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile

exec "$SHELL"

source ~/.bash_profile


$ python -V
Python 3.9.5
```
