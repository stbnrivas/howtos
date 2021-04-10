# ajax for ruby on rails

whenever you doing with ajax it's good to start with the non-ajax version and teh gradually add ajax features...



1. partial templates:

partial are like a method for a view.



2. render

- render plain

```ruby
render plain: 'product not found'
```

- render json

```ruby
render json: @product
```

- render a controller action

```ruby
render :show
```

- render a partial


```ruby
render :form

# render single object
render(Product.new)

# render collections
render(Product.find_by(active: true))
```

3. render_if

```ruby
render_if condition
```

4. render passing object

```ruby
render 'form', order: @order
```


## ajax

```erb
<%= button_to 'Add to Cart', line_items_path(product_id :product), remote: true %>
```

```

def create
	product = Product.find(params[:product_id])
	@line_item = @cart.add_product(product)

	respond_to do |format|
		if @line_item.save
			format.html { redirect_to store_index_url }
			format.js
			format.json { render :show, status: :created, location: @line_item}
		else
			format.html { render :new }
			format.json { render json: @line_item.errors, status: unprocessable_entity }
		end
	end
end
```

```erb
// create.js-erb
cart = document.getElementById("cart")
cart.innerHTML = "<%= j render(@cart) %>"
```