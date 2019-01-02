# installation ndenv

  git clone https://github.com/riywo/node-build.git $(ndenv root)/plugins/node-build

## installation node-build plugin for install node from ndenv

  git clone https://github.com/riywo/ndenv ~/.ndenv
  echo 'export PATH="$HOME/.ndenv/bin:$PATH"' >> ~/.bashrc
  echo 'eval "$(ndenv init -)"' >> ~/.bashrc
  exec $SHELL -l



ndenv [Deprecated] nodenv is better alternative

Please consider to use nodenv. ndenv repository is not maintained actively.



$ git clone https://github.com/nodenv/nodenv.git ~/.nodenv
$ cd ~/.nodenv && src/configure && make -C src
$ echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.bashrc
$ ~/.nodenv/bin/nodenv init

check installation

curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash


update 

$ cd ~/.nodenv
$ git pull


# plugin: node-build https://github.com/nodenv/node-build#installation

mkdir -p "$(nodenv root)"/plugins
git clone https://github.com/nodenv/node-build.git "$(nodenv root)"/plugins/node-build

cd "$(nodenv root)"/plugins/node-build && git pull

