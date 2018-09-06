# installation ndenv

  git clone https://github.com/riywo/node-build.git $(ndenv root)/plugins/node-build

## installation node-build plugin for install node from ndenv

  git clone https://github.com/riywo/ndenv ~/.ndenv
  echo 'export PATH="$HOME/.ndenv/bin:$PATH"' >> ~/.bash_profile
  echo 'eval "$(ndenv init -)"' >> ~/.bash_profile
  exec $SHELL -l
