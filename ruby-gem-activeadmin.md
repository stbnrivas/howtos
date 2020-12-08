# activeadmin

```bash
bundle add activeadmin
```


```ruby
ActiveAdmin.register BeaconReading do

  actions :index, :show, :create, :edit, :update
  #actions :all, :except => [:destroy]

  menu parent: "Parkings"

  permit_params do
    [
      # none
    ]
  end

  config.current_filters = false
  config.batch_actions = false
end
```


