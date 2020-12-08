# gem turbolinks



Turbolinks® makes navigating your web application faster. Get the performance benefits of a single-page application without the added complexity of a client-side JavaScript framework. Use HTML to render your views on the server side and link to pages as usual. When you follow a link, Turbolinks automatically fetches the page, swaps in its <body>, and merges its <head>, all without incurring the cost of a full page load.


```
bundle add turbolinks
bundle install
```



add to file app/assets/javascript/application.js
```

//= require turbolinks
```


add to app/views/layout/application.html.erb
```
<%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```
