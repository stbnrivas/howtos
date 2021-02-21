# python package index

[https://pypi.org](https://pypi.org)


# python and pipenv


1. enable powershell

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

2. install python

https://www.python.org/downloads/release/python-2717/

https://www.python.org/ftp/python/3.7.7/python-3.7.7-amd64.exe


3. pip  (Package Installer for Python)


```bash
sudo apt install python3-pip

# system scope library installation
pip3 install --system pipenv
pip3 install pipenv

# user scope library installation
pip3 install --user pipenv

# installing new packages for system

sudo pip install pyplot


# upgrade
pip3 install --upgrade pip
```

some pip subcommands

```bash
pip3 list --outdate

pip3 --upgrade pyplot
pip3 freeze > requirements.txt     # create a requirements.txt file
# CAUTION:
# create a requirements this way copy ALL your libraries into
# your requirements.txt even you don't use into this project.
# this is why you should use virtualenv with pip

pip3 install -r requirements.txt   # installing all dependencies

pip3 uninstall pyplot
```





pip use a file `requirements.txt` to keep dependencies

```
cat Pipfile


[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]

[packages]

[requires]
python_version = "3.7"
```


pip don't allow to have multiples version of same packages in your system, previously to install a version uninstall existing.



4. virtualenv only (DEPRECATED)

installation

```bash
pip3 install virtualenv

mkdir project ; cd project

# use on the same folder that you have requirements.txt file
ENV_NAME=app_env1
virtualenv $ENV_NAME

source app_env1/bin/activate

deactivate


# delete virtualenv
rm -rf ./app_env1
```


Pipfile is the dedicated file used by the Pipenv virtual environment.



```bash

pip3 freeze > requirements.txt    # create a requirements.txt
pipenv lock -r                    # convert Pipfile and Pipfile.lock into a requirements.txt
pip3 install -r requirements.txt   # install your modules dependencies

pip3 install -r requirements.txt   # installing all dependencies
```



migrating from your requirements.txt to pipenv with Pipfile

```bash
pipenv install -r path/to/requirements.txt # import
rm requirements.txt

cat Pipfile
cat Pipfile.lock
```




5. install pipenv

Pipenv is a new package manager that combines pip and virtualenv into one easy-to-use too. It's easier to work with Pipenv than virtualenv and pip, because it creates the virtual environments for you and manages them too; It's safer to use Pipenv than virtualenv, because every dependency installed has a hash which is saved in a file called Pipfile.lock.

pipenv use the `Pipfile` and `Pipfile.lock` which are designed to replace requirements.txt


the pipenv are store at `~/.local/share/virtualenvs/$name`


```bash
pip3 install pipenv


pipenv --python 3.8    # create a virtual environment and create a Pipfile

pipenv install -r path/to/requirements.txt # import from requirements and create a Pipfile
pipenv install --requirements path/to/requirements.txt # import from requirements and create a Pipfile
rm requirements.txt
pipenv lock

pipenv install requests
pipenv install requests==1.2     # exactly version
pipenv install --dev requests~=1.2  # development

pipenv shell   # activate the virtual environment
```










6. running your app with pipenv

```bash
# pipenv will create a file called Pipfile
pipenv install

# run your app or something without need activate virtualenv first
pipenv run
pipenv run python app.py



# optionally can activate virtualenv
pipenv shell

# optionally can generate requirements.txt file
pipenv lock --requirements > requirements.txt
```




```bash
# specifying versions of python
pipenv --python 3.7.7
pipenv --python 2.7.17

# for dev dependencies
pipenv install --dev

# setting working directory
pipenv install -e .

# show nested dependencies
pipenv graph

# setting specific version of lib
# latest
pipenv install '*'
# lesser than
pipenv install 'django<=2.*'
# exactly to
pipenv install Django = "==1.*"


# install using requirements.txt, this will update into Pipfile
pipenv install -r requirements.txt

pipenv check


# freeze dependences and install from Pipfile.lock
pipenv lock
pipenv install --ignore-pipfile

pipenv uninstall
```













```bash
cat Pipfile

[[source]]
url = "https://pypi.python.org/simple"
verify_ssl = true

[dev-packages]

[packages]

[requires]
python_version = "3.6"
```

```bash
cat Pipfile.lock
```
