# cache on rails



```bash
bin/rails dev:cache
# Development mode is now being cached.
bin/rails dev:cache
# Development mode is no longer being cached.
```

```erb
<ul class="catalog">
  <% cache @products do %>                           <!-- -->
    <% @products.each do |product| %>
      <% cache product do %>                            <!-- -->
      <li>
        <%= image_tag(product.image_url, width: "200px") %>
        <h2><%= product.title %></h2>
        <p>
          <%= sanitize(product.description) %>
        </p>
        <div class="price">
          <%= number_to_currency(product.price) %>
        </div>
      </li>
      <% end %>                                         <!-- -->
    <% end %>
  <% end %>                                          <!-- -->
</ul>
```


## enable / disable cache

```ruby
if Rails.root.join('tmp/caching-dev.txt').exist?
	config.action_controller.enable_fragment_cache_logging = true  # <== enable / disable
	config.action_controller.perform_caching = true

	config.cache_store = :memory_store

end
```

```log
Read fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/1-20210319185129957502 (0.3ms)
Write fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/1-20210319185129957502 (0.2ms)
Read fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/2-20210319185129966977 (0.1ms)
Write fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/2-20210319185129966977 (0.2ms)
Write fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/query-472c5e944ebe4d9a8d77c3b8cccbda69-2-20210319185129966977 (0.3ms)


# nest times only read from cache:

  ↳ app/views/store/index.html.erb:8
Read fragment views/store/index:190ac654b012eff71c8d1f9e49bdbdb8/products/query-472c5e944ebe4d9a8d77c3b8cccbda69-2-20210319185129966977 (2.1ms)
```