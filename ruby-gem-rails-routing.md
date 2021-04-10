# rails routes


## routing controller types

- controller action based

```ruby
# routes.rb

get 'statistics',            to: 'statistics#last'
get 'statistics/last-week',  to: 'statistics#last_week'
get 'statistics/last-month', to: 'statistics#last_month'
```



- controller resource based

```ruby
# routes.rb

resources :products

resources :products, except: [:update, :destroy]
resources :products, only: [:index, :show]
```


```
    prefix |   METHOD   |                               |  controller#action
-------------------------------------------------------------------------
   products    GET        /products(.:format)              products#index
               POST       /products(.:format)              products#create
new_product    GET        /products/new(.:format)          products#new
dit_product    GET        /products/:id/edit(.:format)     products#edit
    product    GET        /products/:id(.:format)          products#show
               PATCH      /products/:id(.:format)          products#update
               PUT        /products/:id(.:format)          products#update
               DELETE     /products/:id(.:format)          products#destroy
```



- adding additional actions to resource

```ruby
# routes.rb

resources :products do
  member do
    get 'inventory_status' # /products/:id/inventory_status
  end
  get :sales_statistics, on: :member # /producs/:product_id/sales_statistics CAUTION params[:id] not available


  collection do
    get 'search'
  end
  get :best_seller, on: :collection
end
```
```
inventory_status_product     GET    /products/:id/inventory_status(.:format)    products#inventory_status
sales_statistics_product     GET    /products/:id/sales_statistics(.:format)    products#sales_statistics
search_products              GET    /products/search(.:format)                  products#search
best_seller_products         GET    /products/best_seller(.:format)             products#best_seller
```




- nested resources route

```ruby
# routes.rb
resources :products do
  resources :reviews
end
```
```
    product_reviews         GET       /products/:product_id/reviews(.:format)            reviews#index
                            POST      /products/:product_id/reviews(.:format)            reviews#create
 new_product_review         GET       /products/:product_id/reviews/new(.:format)        reviews#new
edit_product_review         GET       /products/:product_id/reviews/:id/edit(.:format)   reviews#edit
     product_review         GET       /products/:product_id/reviews/:id(.:format)        reviews#show
                            PATCH     /products/:product_id/reviews/:id(.:format)        reviews#update
                            PUT       /products/:product_id/reviews/:id(.:format)        reviews#update
                            DELETE    /products/:product_id/reviews/:id(.:format)        reviews#destroy
                            GET       /products(.:format)                                products#index
                            POST      /products(.:format)                                products#create
                            GET       /products/new(.:format)                            products#new
                            GET       /products/:id/edit(.:format)                       products#edit
                            GET       /products/:id(.:format)                            products#show
                            PATCH     /products/:id(.:format)                            products#update
                            PUT       /products/:id(.:format)                            products#update
                            DELETE    /products/:id(.:format)                            products#destroy
```




- routing concerns

```ruby
# routes.rb

## single concern
concern :reviewable do
  resources :reviews
end

resources :products, concern: :reviewable

## multiple concern
concern :image_attachable do
  resources :images, only: :index
end


resources :products, concern: [:reviewable, :image_attachable]

# this equivalent to
resources :products do
  resources :reviews
end
```



```
                           GET       /products(.:format)                             products#index {:concern=>:reviewable}
                           POST      /products(.:format)                             products#create {:concern=>:reviewable}
                           GET       /products/new(.:format)                         products#new {:concern=>:reviewable}
                           GET       /products/:id/edit(.:format)                    products#edit {:concern=>:reviewable}
                           GET       /products/:id(.:format)                         products#show {:concern=>:reviewable}
                           PATCH     /products/:id(.:format)                         products#update {:concern=>:reviewable}
                           PUT       /products/:id(.:format)                         products#update {:concern=>:reviewable}
                           DELETE    /products/:id(.:format)                         products#destroy {:concern=>:reviewable}
```


- shallow route nesting

```ruby
# routes.rb

resources :products, shallow: true do
  resources :reviews
end
```


```
product_reviews         GET    /products/:product_id/reviews(.:format)              previews#index
                        POST   /products/:product_id/reviews(.:format)              previews#create
 new_product_review     GET    /products/:product_id/reviews/new(.:format)          previews#new
 edit_review            GET    /reviews/:id/edit(.:format)                          previews#edit
 review                 GET    /reviews/:id(.:format)                               previews#show
                        PATCH  /reviews/:id(.:format)                               previews#update
                        PUT    /reviews/:id(.:format)                               previews#update
                        DELETE /reviews/:id(.:format)                               previews#destroy

```






## namespace and scope

namespace vs scope

```ruby
namespace :blog do
  resources :posts
end
#      blog_posts   GET       /blog/posts(.:format)               blog/posts#index
#                   POST      /blog/posts(.:format)               blog/posts#create
#   new_blog_post   GET       /blog/posts/new(.:format)           blog/posts#new
#  edit_blog_post   GET       /blog/posts/:id/edit(.:format)      blog/posts#edit
#       blog_post   GET       /blog/posts/:id(.:format)           blog/posts#show
#                   PATCH     /blog/posts/:id(.:format)           blog/posts#update
#                   PUT       /blog/posts/:id(.:format)           blog/posts#update
#                   DELETE    /blog/posts/:id(.:format)           blog/posts#destroy


scope :blog do
  resources :posts
end
#           posts   GET       /blog/posts(.:format)                    posts#index
#                   POST      /blog/posts(.:format)                    posts#create
#        new_post   GET       /blog/posts/new(.:format)                posts#new
#       edit_post   GET       /blog/posts/:id/edit(.:format)           posts#edit
#            post   GET       /blog/posts/:id(.:format)                posts#show
#                   PATCH     /blog/posts/:id(.:format)                posts#update
#                   PUT       /blog/posts/:id(.:format)                posts#update
#                   DELETE    /blog/posts/:id(.:format)                posts#destroy
```









[https://devblast.com/b/rails-5-routes-scope-vs-namespace](https://devblast.com/b/rails-5-routes-scope-vs-namespace)

- namespace

```ruby
namespace :admin do
  resources :users
end
```


Prefix Verb   URI Pattern                Controller#Action
admin_users GET    /admin/users(.:format)     admin/users#index
            POST   /admin/users(.:format)     admin/users#create
admin_user  GET    /admin/users/:id(.:format) admin/users#show
            PATCH  /admin/users/:id(.:format) admin/users#update
            PUT    /admin/users/:id(.:format) admin/users#update
            DELETE /admin/users/:id(.:format) admin/users#destroy




- scope no options

```ruby
scope :admin do
  resources :users
end
```


Prefix Verb   URI Pattern                Controller#Action
 users GET    /admin/users(.:format)     users#index
       POST   /admin/users(.:format)     users#create
  user GET    /admin/users/:id(.:format) users#show
       PATCH  /admin/users/:id(.:format) users#update
       PUT    /admin/users/:id(.:format) users#update
       DELETE /admin/users/:id(.:format) users#destroy


- scope with options  {module,path,as}

```ruby
scope module: 'admin' do
  resources :users
end
```

```
Prefix Verb   URI Pattern          Controller#Action
---------------------------------------------------------
 users GET    /users(.:format)     admin/users#index
       POST   /users(.:format)     admin/users#create
  user GET    /users/:id(.:format) admin/users#show
       PATCH  /users/:id(.:format) admin/users#update
       PUT    /users/:id(.:format) admin/users#update
       DELETE /users/:id(.:format) admin/users#destroy
```

```ruby
scope module: 'admin', path: 'fu' do
  resources :users
end
```
```
Prefix Verb   URI Pattern             Controller#Action
 users GET    /fu/users(.:format)     admin/users#index
       POST   /fu/users(.:format)     admin/users#create
  user GET    /fu/users/:id(.:format) admin/users#show
       PATCH  /fu/users/:id(.:format) admin/users#update
       PUT    /fu/users/:id(.:format) admin/users#update
       DELETE /fu/users/:id(.:format) admin/users#destroy
```

```ruby
scope module: 'admin', path: 'fu', as: 'cool' do
  resources :users
end
```
```
    Prefix      Verb     URI Pattern                       Controller#Action
-----------------------------------------------------------------------------
     cool_users GET     /fu/users(.:format)                admin/users#index
                POST    /fu/users(.:format)                admin/users#create
  new_cool_user GET     /fu/users/new(.:format)            admin/users#new
 edit_cool_user GET     /fu/users/:id/edit(.:format)       admin/users#edit
      cool_user GET     /fu/users/:id(.:format)            admin/users#show
                PATCH   /fu/users/:id(.:format)            admin/users#update
                PUT     /fu/users/:id(.:format)            admin/users#update
                DELETE  /fu/users/:id(.:format)            admin/users#destroy
```