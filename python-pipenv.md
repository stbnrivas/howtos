
# python and pipenv


1. enable powershell 

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

2. install python

https://www.python.org/downloads/release/python-2717/

https://www.python.org/ftp/python/3.7.7/python-3.7.7-amd64.exe



3. install pipenv

Pipenv is a new package manager that combines pip and virtualenv into one easy-to-use too


```bash
# only if need
pip install --upgrade pip

# system scope library installation
pip install --system pipenv
pip install pipenv

# user scope library installation
pip install --user pipenv

# specifying versions of python
$ pipenv --python 3.7.7
$ pipenv --python 2.7.17

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





```
pipenv
pipenv shell

pipenv run python

# check version in use
import sys
sys.executable
```


pipenv create a file called Pipfile like but the env it is no assocciated to a project... it will bi associated to 

Virtualenv location: C:\Users\stbn\.virtualenvs\stbn-iSMLspIT
Creating a Pipfile for this project...
Successfully created virtual environment!




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
