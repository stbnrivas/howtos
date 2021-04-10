# forms with rails


## form_tag, form_for

Before form_with was introduced in Rails 5.1 its functionality used to be split between form_tag and form_for. Both are now soft-deprecated.


## form_with

```
<%= form_with do |form| %>
  Form contents
<% end %>
```

rails form generate `authenticity_token` security feature called `cross-site request forgery protection`

```html
<form accept-charset="UTF-8" action="/" method="post">
  <input name="authenticity_token" type="hidden" value="J7CBxfHalt49OSHp27hblqK20c9PgwJ108nDHX/8Cts=" />
  Form contents
</form>
```


- basic example
```erb
<%= form_for(@product) do |f| %>

<% end %>
```

- giving an url
```erb
# creating new product
<%= form_for(model: @product, url: products_path) do |f| %> # equivalent long style
<%= form_for(model: @product) do |f| %>                     # equivalent short style
<% end %>


# editing existing product
<%= form_for(model: @product, url: product_path(@product), method: "patch") do |f| %> # equivalent long style
<%= form_for(model: @product) do |f| %>                                               # equivalent short style
<% end %>
```


- dealing with namespaces
```erb
<%= form_with model: [:admin, @article] %>                                            # equivalent short style
<% end %>
```

- specifying the method
```erb
<%= form_with(url: search_path, method: "patch") %>                                     # equivalent short style
<% end %>
```


## fields

```erb
<%= form.text_area :message, size: "70x5" %>

<%= form.hidden_field :parent_id, value: "foo" %>
<%= form.password_field :password %>
<%= form.number_field :price, in: 1.0..20.0, step: 0.5 %>
<%= form.range_field :discount, in: 1..100 %>
<%= form.date_field :born_on %>
<%= form.time_field :started_at %>
<%= form.datetime_local_field :graduation_day %>
<%= form.month_field :birthday_month %>
<%= form.week_field :birthday_week %>
<%= form.search_field :name %>
<%= form.email_field :address %>
<%= form.telephone_field :phone %>
<%= form.url_field :homepage %>


City.order(:name).to_a # [ <City id: 3, name: "Berlin">, <City id: 1, name: "Chicago">, <City id: 2, name: "Madrid"> ]

<%= form.collection_radio_buttons :city_id, City.order(:name), :id, :name %>

<%= form.collection_check_boxes :city_id, City.order(:name), :id, :name %>

<%= form.select :city, ["Berlin", "Chicago", "Madrid"] %>
<%= form.select :city, [["Berlin", "BE"], ["Chicago", "CHI"], ["Madrid", "MD"]] %>
<%= form.select :city, [["Berlin", "BE"], ["Chicago", "CHI"], ["Madrid", "MD"]], selected: "CHI" %>
<%=  form.select :city,{ "Europe" => [ ["Madrid", "MD"] ], "North America" => [ ["Chicago", "CHI"] ]}, selected: "CHI" %>

<%= form.collection_select :city_id, City.order(:name), :id, :name %>

<%= form.file_field :picture %>
```


```ruby
class Order < ApplicationRecord
  enum pay_type: {
    "Check" => 0,
    "Credit card" => 1,
    "Purchase Order" => 2
  }
end
```


```
<%= form_with(model: order, local: true) do |form| %>
  <% if order.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(order.errors.count, "error") %> prohibited this order from being saved:</h2>

      <ul>
        <% order.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="field">
    <%= form.label :name %>
    <%= form.text_field :name, size: 40 %>
  </div>

  <div class="field">
    <%= form.label :address %>
    <%= form.text_area :address, rows: 3, cols: 40 %>
  </div>

  <div class="field">
    <%= form.label :email %>
    <%= form.text_field :email, size: 40 %>
  </div>

  <div class="field">
    <%= form.label :pay_type %>
    <%= form.select :pay_type, Order.pay_types.keys, prompt: 'Select a payment method' %>
  </div>

  <div class="actions">
    <%= form.submit %>
  </div>
<% end %>
```