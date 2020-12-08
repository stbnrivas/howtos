# add support bootstrap to rails





```
cd rails-app

#search version of bootstrap
npm view $module-name versions  --json

[
  ...
  "4.5.3",
  "5.0.0-alpha1",
  "5.0.0-alpha2"
]



yarn add bootstrap@4.5.3 jquery popper.js


touch config/webpack/environment.js
```


config/webpack/environment.js
```
const { environment } = require('@rails/webpacker')
const webpack = require('webpack')

environment.plugins.prepend(
    'Provide',
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery',
      jquery: 'jquery',
      'window.jQuery': 'jquery',
      Popper: ['popper.js', 'default'],
    })
)

module.exports = environment
```



if you use css

mv app/assets/stylesheets/application.css
```
*= require bootstrap
*= require_tree .
*= require_self

```


if you use scss

```
mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
```

```
@import "bootstrap-sprockets";
@import "bootstrap";
```
