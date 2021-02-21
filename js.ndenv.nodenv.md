# installation ndenv


```bash
git clone https://github.com/nodenv/nodenv.git ~/.nodenv
cd ~/.nodenv && src/configure && make -C src
echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.bashrc
~/.nodenv/bin/nodenv init
```

## check installation

```bash
curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash
```

## update

```bash
$ cd ~/.nodenv
$ git pull
```

# plugin: node-build https://github.com/nodenv/node-build#installation

```bash
mkdir -p "$(nodenv root)"/plugins
git clone https://github.com/nodenv/node-build.git "$(nodenv root)"/plugins/node-build

cd "$(nodenv root)"/plugins/node-build && git pull
```



## location of node_modules global


```bash
npm get prefix

#~/.nodenv/versions/12.19.0
```


```
~/.nodenv/versions/${version}/lib/node_modules/npm/node_modules

~/.nodenv/versions/12.19.0/lib/node_modules/npm/node_modules
```



```bash
npm install -g watchy

nodenv rehash
whereis watchy
```