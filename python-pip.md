# intro

pip     is like gem in ruby
pip3       same pip but for python3

pyenv   is like rbenv in ruby
pipenv  is like bundler in ruby


# pip - the python package installer



```bash
pip help

pip search flask

pip install flask
pip uninstall flask


pip install -Iv 'flask==0.12'
pip install 'stevedore>=1.3.0,<1.4.0'


pip install -Iv 'flask==0.10.1'
```



```bash
# install globally
sudo -H pip install keyring


# pip install into home without privileges
pip install --user data-catalog-dcat-validator
pip uninstall data-catalog-dcat-validator
```




```bash
pip3 freeze > requirements.txt  # Python3
pip  freeze > requirements.txt  # Python2

pip freeze --local > requirements.txt
```



```bash
pip install -r requirements.txt
```


```bash
pip install --upgrade pip
```



# virtualenv



```bash
pip install virtualenv

mkdir -p project-folder/Enviroments
cd proyect-folder/Enviroments

which python

virtualenv project1_env
source project1_env/bin/activate

which python

deactivate 

which python
```



```
virtualenv -p /user/bin/python2.6 py26_env
```



# to update requirements.txt


```
pip install pur
pur -r requirements.txt
```