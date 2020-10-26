
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

Por defecto, Pipenv guarda todos tus entorno virtuales en un solo lugar. Usualmente esto no es un problema, pero si te gustaría cambiarlo para comodidad de desarrollo, o si esta causando issues en servidores de construcción puedes setear PIPENV_VENV_IN_PROJECT para crear un entorno virtual dentro de la raíz de tu proyecto.

It's easier to work with Pipenv than virtualenv and pip, because it creates the virtual environments for you and manages them too;

It's safer to use Pipenv than virtualenv, because every dependency installed has a hash which is saved in a file called Pipfile.lock.

```bash
# only if need
pip install --upgrade pip

# system scope library installation
pip install --system pipenv
pip install pipenv

# user scope library installation
pip install --user pipenv
```

4. migrating from virtualenv to pipenv

```bash
# use on the same folder that you have requirements.txt file
pipenv install

rm requirements.txt

cat Pipfile
cat Pipfile.lock
```



5. running your app with pipenv

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
