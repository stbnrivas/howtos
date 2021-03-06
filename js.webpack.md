# webpack

webpack is a bundler for js script images css typescript ... webpack is an advance from gulp or trunt because, webpack can do task like gulp and group like minifyjs but can handle js dependences 

webpack is a bundler of js dependences minifying and join all project to one or multiples js files by default webpack doesn't build css from sass, or minify html, instead build sass file and convert to js that is executed without mention css or sass file without link tag into header of html document


## concepts

- entry: 
has one or multiples entry poing we start to build dependency graph

- output: 
where destination to solve your output 

- loaders: 
outbox webpack only work with js and json files, loaders handle source files to transform certain types modules

- plugins: 
loders work with source files while plugins can works with task injection of environment variables or like minify css js or image manipulations to optimice

- mode: development|production


## webpack installation

```bash
npm install --global webpack webpack-cli
npm install --save-dev webpack webpack-cli 
```

```bash
webpack init 
```

webpack with config file we

webpack loaders

```bash
webpack init
webpack migrate
```

## webpack from CLI

```bash
webpack --version
webpack --mode development --entry ./src/js/app.js --output ./src/js/app.bundle.js
```

```javascript
// src/js/app.js
var _ = require("underscore")
_.each([1, 2, 3], alert);
console.log("it works")
```


```html
<!-- src/index.html -->
<html>
<head>
	<meta charset="UTF-8">
	<title>test webpack</title>
</head>
<body>
  <!-- not work -->
  <!-- <script src="./js/app.js"></script> -->

  <!-- it works -->
	<script src="./js/app.bundle.js"></script>
</body>
</html>
```



## webpack using webpack.config.js

```bash
mkdir webpack-project && cd webpack-project
mkdir -p src/js src/css src/scss src/images
touch src/js/app.js src/scss/app.scss src/index.htm
nmp init -y
echo "node_modules" >> .gitignore
nmp install --save-dev webpack webpack-cli # because was added to package.json
webpack init
```

```javascript
//webpack.config.js
const path = require('path');
module.exports = {
  mode: 'development',
  entry: './src/js/app.js',
  output: {
    path: path.resolve(__dirname, 'src/js'),
    filename: 'app.bundle.js'
  },
  watch: false,
};

// helper.js
var helper = "hello, may can i help you"
exports.hello = function(name){
    console.log(helper)
}
// app.js
var helper = require('./helper')
helper.hello("unknown")
```

```bash
# taking default config file
webpack
webpack -p
# specifyin config file
webpack --config webpack.dev.config.js
# watch mode
webpack --watch
```

### with css loader that inject styles into js

```bash
npm install --global style-loader css-loader
´´´

```javascript
// webpack.config.js
const path = require('path')
module.exports = {
    mode:'development',
    entry:'./src/js/app.js',
    output:{
        path: path.resolve(__dirname,'src/js'),
        filename: 'app.bundle.js'
    },
    module: {
        rules: [
            { test: /\.css$/, use: ['style-loader', 'css-loader' ] }
        ],
    }
}
```

### with sass loader that compile scss -> css and inject styles into js

```bash
npm install --global style-loader css-loader sass-loader
```

```javascript
const path = require('path')
module.exports = {
    mode: 'development',
    watch: false,
    entry: './src/js/app.js',
    output: {
        path: path.resolve(__dirname,'src/js'),
        filename: 'app.bundle.js',
    },
    module:{
        rules:[
            {test:/\.scss$/,use:['style-loader','css-loader','sass-loader']},
        ]
    }
}
```


### babel transpilacion

```bash
npm install --save-dev babel-loader babel-core babel-preset-env
touch .babelrc
```

file .babelrc
```json
{
  "presets": [
  "env"
  ]
}
```

```bash
webpack --mode production --module-bind js=babel-loader
```


### webpack dev server

```bash
npm install --save-dev webpack-dev-server

webpack-dev-server --mode development --open
``` 


### interesting plugins


```bash
# clean dist folder each new build
npm install --save-dev clean-webpack-plugin

npm install --save-dev css-loader     # css files
npm install --save-dev style-loader   # styles inline
npm install --save-dev mini-css-extract-plugin   # extract css and set in css fil
npm install --save-dev node-sass sass-loader  # 
npm install --save-dev postcss-loader   # 

npm install --save-dev file-loader resolve-url-loader  # 

npm install --save-dev image-webpack-loader   # 


npm install --save-dev html-loader html-webpack-plugin  # 


npm install --save-dev postcss-loader autoprefixer  # 

npm install --save-dev   # 




``` 
