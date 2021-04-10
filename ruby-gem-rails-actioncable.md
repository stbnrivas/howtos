# action cable



1. generate channel

```bash
bin/rails generate channel products

# Running via Spring preloader in process 23421
#       invoke  test_unit
#       create    test/channels/products_channel_test.rb
#       create  app/channels/products_channel.rb
#    identical  app/javascript/channels/index.js
#    identical  app/javascript/channels/consumer.js
#       create  app/javascript/channels/products_channel.js
```

2. create channel

```ruby
class ProductsChannel < ApplicationCable::Channel
  def subscribed
    stream_from "products"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end
```

3. OPTIONAL enable/disable for your enviroment if you are using differents hosts

```ruby
#config/enviroments/development.rb
config.action_cable.disable_request_forgery_protection = true
```

4. broadcast data

```ruby
  def update
    respond_to do |format|
      if @product.update(product_params)
        format.html { redirect_to @product, notice: "Product was successfully updated." }
        format.json { render :show, status: :ok, location: @product }

		#
        @products = Product.all.order(:title)
        ActionCable.server.broadcast 'products', html: render_to_string('store/index', layout: false)
        #
      else
        format.html { render :edit, status: :unprocessable_entity }
        format.json { render json: @product.errors, status: :unprocessable_entity }
      end
    end
  end
```

5. parse received data into client

```js
import consumer from "./consumer"

consumer.subscriptions.create("ProductsChannel", {
  connected() {
    // Called when the subscription is ready for use on the server
    console.log("connected to channel: `ProductsChannel`")
  },

  disconnected() {
    // Called when the subscription has been terminated by the server
    console.log("disconnected from channel: `ProductsChannel`")
  },

  received(data) {
    // Called when there's incoming data on the websocket for this channel
    const elementToReplace = document.querySelector("main.store")
    if(elementToReplace) {
    	elementToReplace.innerHTML = data.html
    }
  }
});

```

6. look for log messages which channel is working

```
Started GET "/cable" for ::1 at 2021-03-21 17:23:21 +0100
Started GET "/cable/" [WebSocket] for ::1 at 2021-03-21 17:23:21 +0100
Successfully upgraded to WebSocket (REQUEST_METHOD: GET, HTTP_CONNECTION: keep-alive, Upgrade, HTTP_UPGRADE: websocket)
ProductsChannel is transmitting the subscription confirmation
ProductsChannel is streaming from products

```
