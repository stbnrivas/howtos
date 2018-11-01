# installation

	```javascript
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
	```javascript
	npm init
	npm init --yes
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

when there is a package.json into folder you can install dependences with 

	```bash
	npm install [--production]
	```


## searchin for package

	```javascript
	// search
	npm search $module-name
	// installation 
	npm install --save $module-name
	npm install $module-name		// equivalent --save
	npm install --save-dev			// save dependence like as development dependence
	npm install -g --global			// you can see folder with $ npm root -g
	// specifing specific version
	npm install lodash@4.17.3
	// install from github repo
	npm install git://github.com/substack/node-browserify.git
	npm install git://github.com/Marak/colors.js#v0.6.0
	// uninstall 
	npm uninstall $module-name
	npm uninstall $module-name
	npm uninstall -g $module-name // uninstall from global
	// update
	npm update webpack
	```

## seeing dependences tree

	```bash
	npm list
	npm list --depth 1
	```


## scripts into package.json

you can map command that will be execute via npm modifing package.json


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
	  "keywords": [],
	  "author": "stbrivas@gmail.com",
	  "license": "ISC",
	  "dependencies": {
	    "lodash": "^4.17.11",
	    "webpack": "^4.23.1"
	  },
	  "devDependencies": {
	    "live-server": "^1.2.0"
	  }
	}
	```

and you can run with 

	```bash
	npm build
	npm server
	npm test
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