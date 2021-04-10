# installation

```bash
npm config ls -l
# set or get
npm config set init-author-name "stbnrivas@gmail.com"
npm config set init-license
npm config get init-author-name
# update npm
npm update npm -g
```

# using npm
initialization

```bash
npm init
npm init --yes
echo "node_modules" > .gitignore
```

below command create a json config file

```json
{
  "name": "test-npm",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "stbrivas@gmail.com",
  "license": "ISC"
}
```

new packages installation using install



npm install takes exclusive, optional flags which save or update the package version in your main package.json:
when there is a package.json into folder you can install dependences with and by default dependences will be added

```bash
npm install
	# -S --save: deprecated now by default package will add in your dependencies.
	#     --no-save

	# -P  --save-prod
	# -D  --save-dev	   package will add in your devDependencies.
	# -O  --save-optional  package will add in your optionalDependencies.
	# -E  --save-exact
	# -B  --save-bundle
	# 	  --dry-run
```


```bash
npm install babel-cli babel-preset-stage-0 babel-preset-es2015 --save-dev
```


## searching for package

```bash
# search
npm search $module-name
# view versions
npm view $module-name versions  --json


npm root
# ~/node_modules
npm root -g
# ~/.nodenv/versions/12.19.0/lib/node_modules


# installation globally `/user/local/lib/node_modules` `/user/local/lib/node`
npm install -g       $package
npm install --global $package

# installation locally `.\node_modules`
npm install          $package
```



```bash
# installation package especifying environment where it will be installed

npm install                 $package
npm install --save          $package

# {
#  "name":
#  "version":
#  "description":
#  "main":
#  "scripts": {}
#  "dependencies": {
#    "babel-cli": "^6.26.0"
#  }
# }


npm install --save-prod     $package

# {
#  "name":
#  "version":
#  "description":
#  "main":
#  "scripts": {}
#  "dependencies": {
#    "babel-cli": "^6.26.0"
#  }
# }

npm install --save-dev      $package

# {
#  "name":
#  "version":
#  "description":
#  "main":
#  "scripts": {}
#  "dependencies": {}
#  "devDependencies": {
#    "babel-cli": "^6.26.0"
#  }
# }

npm install --save-optional $package

npm install --no-save       $package


# major.minor.patch  1.2.3
# without   exactly the same version
# caret `^` (less restricted) all minor and patches is OK => 1.2.3, 1.2.4, 1.3.0
# tilde `~` (more restricted) all patches is OK           => 1.2.3, 1.2.4


# specifing specific version
npm install lodash@4.17.3


# install from github repo
npm install git://github.com/substack/node-browserify.git
npm install git://github.com/Marak/colors.js#v0.6.0


# uninstall
npm uninstall $module-name
npm uninstall $module-name
npm uninstall -g       $module-name // uninstall from global
npm uninstall --global $module-name // uninstall from global
# update
npm update webpack
# audit
npm audit
```

## seeing dependences tree

```bash
npm list
npm list --depth 1
```

## seeing outdates

```bash
npm outdates -g
npm outdates --global

npm outdates
```


## other npm topics


- manage cache

```bash
npm cache verify
npm cache clean --force
```

- audit dependencies

```bash
npm audit
```




## scripts into package.json

you can map command that will be execute via npm or directly modifing package.json


```json
{
  "name": "test-npm",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",

  "scripts": {
    "build": "echo \"webpack\" && exit 1",
    "server": "live-server",
    "test": "test",
  },

  /* ... */
}
```

and you can run with

```bash
npm build
npm server
npm test
```



## npx - execute npm package binaries

```bash
npx -p        @angular/cli ng new myapp
npx --package @angular/cli ng new myapp

# eXecute a commando into of package selected
```

```bash
npx cowsay hello!
```


the point is you can run npm package binary without install into your node_modules
to test or to keep free your dependencies...

```bash
npx yarn
```


also can use npx into package.json

```bash
{
  "name": "test-npm",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",

  "scripts": {
    "create-angular-app": "npx --package @angular/cli ng new myapp"
  }

  /* ... */
}
```




# interesting packages

- lodash: A JavaScript utility library delivering consistency, modularity, performance, & extras. Lodash makes JavaScript easier by taking the hassle out of working with arrays, numbers, objects, strings, etc. Things like Iterating arrays, objects, & strings, Manipulating & testing values, Creating composite functions


	npm install lodash

```javascript
const _ = require('lodash')
const numbers = [33,45,68,78]
_.each(numbers,function(number,i){
	console.log(number )
})
```

 - nodemon: Nodemon is a utility that will monitor for any changes in your source and automatically restart your server. Perfect for development with express...

```bash
npm install nodemon --save-dev
# nodemon [your node app]
nodemon ./server.js localhost 8080
```

- live-server: This is a little development server with live reload capability. Use it for hacking your HTML/JavaScript/CSS files, but not for deploying the final site.

```bash
live-server --port=8080 --host=localhost
```








# yarn

js package manager alternative to npm created by facebook. add standarized lockfile yarn.lock for cross package compatibility. is a bit faster but not by much


# installation

```bash
npm install -g yarn
yarn -v
yarn --help
```



```bash
yarn init
yarn init -y
#
yarn config set init-license MIT
yarn config get init-license
yarn config delete init-license
#
yarn add vue
yarn add --dev vue
yarn add lodash@4.17.3
yarn install
yarn remove vue
#
yarn global add nodemon
yarn global bin
#
yarn global remove nodemon
#
yarn check
#
yarn list # see global dependencies
yarn list depth=1 # see global dependencies
#
yarn outdated
yarn outdated lodash
yarn upgrade lodash@4.17.4
#
yarn licenses list
#
yarn pack # wrote package.tar.gz
#
yarn cache list
yarn cache clean
```











# parcel


# ni