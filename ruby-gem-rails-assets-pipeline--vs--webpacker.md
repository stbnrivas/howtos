# webpacker vs asset pipeline

https://www.youtube.com/watch?v=2v4ySqyua1s

In truth assets pipeline works in rails is required, the title would be webpacker vs no webpacker









## the assets pipeline

the asset pipeline provides a framework to concatenate and minify or compress javascript and css assets. Sprockets concatenates all JavaScript files into one master .js file and all CSS files into one master .css file. Rails inserts an SHA256 fingerprint into each filename so that the file is cached by the web browser. You can invalidate the cache by altering this fingerprint, which happens automatically whenever you change the file contents.

https://guides.rubyonrails.org/asset_pipeline.html

The asset pipeline is implemented by the sprockets-rails gem, and is enabled by default. because this which you will see a sha as suffix for assets to make cache easier this process is called fingerprinted

if using the `turbolinks` gem, which is included by default in Rails, then include the 'data-turbolinks-track' option which causes turbolinks to check if an asset has been updated and if so loads it into the page:


In previous versions of Rails, all assets were located in subdirectories of public such as images, javascripts and stylesheets. With the asset pipeline, the preferred location for these assets is now the `app/assets` directory. Files in this directory are served by the Sprockets middleware.


Pipeline assets can be placed inside an application in one of three locations:
- `app/assets`  assets that are owned by the application, images, JavaScript files, or stylesheets.
- `lib/assets`
- `vendor/assets`




for js files looks like:

```
# if files exist
app/assets/javascripts/home.js
lib/assets/javascripts/moovinator.js
vendor/assets/javascripts/slider.js
vendor/assets/somepackage/phonebox.js
app/assets/javascripts/sub/something.js

# are referenced like this into file app/assets/javascript/application.js
//= require home
//= require moovinator
//= require slider
//= require phonebox
//= require sub/something
```

for sass file looks like:

```
# When using the asset pipeline, paths to assets must be re-written and sass-rails provides -url and -path helpers

@import "core/variables";
@import "bootstrap";
```

for css renamed as css.erb

```
.class { background-image: url(<%= asset_path 'image.png' %>) }

#logo { background: url(<%= asset_data_uri 'logo.png' %>) }
```


for images

```
app/assets/images

<%= image_tag "rails.png" %>
```


### the assets pipeline concepts

the assets pipeline has:

- preprocessor

run when the file is loaded for example the DirectiveProcessor take in charge load lodash:

```
//= require lodash
```

- transformers
```
.coffee -> .js
```

- postprocessors

postprocessor run after transformers, autoprefixer is an postprocessor

```
:fullscreen a { }

/* generate */

:-webkit-full-screen a {}
:-moz-full-screen a {}
:-ms-full-screen a {}
:full-screen a {}

```

- compressors

uglyfier is a compressor, it make things smaller

- exporters



## assets task & assets generators

```
bin/rails -T:

bin/rails assets:clean[keep]                 # Remove old compiled assets
bin/rails assets:clobber                     # Remove compiled assets
bin/rails assets:environment                 # Load asset compile environment
bin/rails assets:precompile                  # Compile all the assets named in config.assets.precompile


# assets task
bin/rails g assets --help


bin/rails g assets    posts
bin/rails g assets -j posts
bin/rails g assets -y posts
bin/rails g assets -je=JAVASCRIPT_ENGINE posts
bin/rails g assets -se=STYLESHEET_ENGINE posts
bin/rails g assets -se=scss posts

 -j, [--javascripts], [--no-javascripts]        # Generate JavaScripts
  -y, [--stylesheets], [--no-stylesheets]        # Generate Stylesheets
                                                 # Default: true
  -je, [--javascript-engine=JAVASCRIPT_ENGINE]   # Engine for JavaScripts
  -se, [--stylesheet-engine=STYLESHEET_ENGINE]   # Engine for Stylesheets
                                                 # Default: scss

```


## assets pipeline into scss files

```scss
.logo{
	width:100px;
	height:100px;
	background-image: url("layout/logo.png")        /* BAD   */
	background-image: asset-url("layout/logo.png")  /* RIGHT */

	content: asset-path("layout/logo.png")          /* to get url */
	content: asset-data-url("layout/logo.png")
}
```

















## webpacker

webpack is a static module bundler for moderm js apps
webpacker is just a wrapper for webpack


### webpack concepts

- entry points (app/javascript/packs in rails)
   + .vue
   + .js
   + .scss
   + .png

- loaders

  + vue-loader
  + postcss-loader

```js
module.exports = {
	module: {
		rules: [
			{
				test: /\.scss$/,
				use: [
					// run in reverse order
					{ loader: "style-loader"}, // add css to the DOM by injecting a <style> tag
					{ loader: "css-loader"},   // interprets @import and url() and resolves
					{ loader: "sass-loader"},  // compiles SASS to CSS using node sass
				]
			}
		]
	}
}
```

- outputs













# using assets pipeline into rails


|                                   |             assets pipeline               |          webpacker               |
|-----------------------------------|-------------------------------------------|----------------------------------|
| where are assets located?         |             `app/assets/`                 | `app/javascript/ even files`     |
|                                   |                                           |                                  |
| where after compile, fingerprinted|             `public/assets`               | `public/packs/`                  |
|                                   |                                           |                                  |
| how to do componets?              |                                           |                                  |
|                                   |                                           |                                  |
| tags for styles                   | <%=stylesheet_link_tag 'application' %>   | <%=stylesheet_pack_tag 'app'%>   |
|                                   |                                           |                                  |
| tags for                          | <%=javascript_include_tag 'application' %>| <%= javascript_pack_tag 'app'%>  |
|                                   |                                           |                                  |
| what happens when add an asset?   | sprockets concatenante (multiples times)  | webpack add an unique dependence |





# using webpacker into rails

```
rails new using-webpacker


cat using-webpacker/package.json

cat using-webpacker/config/webpacker.yml

ls  using-webpacker/config/webpack
	development.js
	environment.js
	production.js
	test.js
```



```
rails webpacker:install:stimulus
rails webpacker:install:vue
rails webpacker:install:react
rails webpacker:install:angular
```





```
// app/javascript/pack/application.js
<%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reaload' %>
<%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reaload' %>
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```