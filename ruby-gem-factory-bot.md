# factory bot && faker win win




```bash
bundle add faker
bundle add factory_bot_rails
```


```ruby
gem "factory_bot_rails", "~> 5.0"
gem "faker", "~> 1.9"
```

## a example


```ruby
require 'faker'

FactoryBot.define do

  factory :dependent_model do
    # never fill `id` it will be feed by db
    # association :author, factory: :user, last_name: "Writely" TODO
    trait :status_free do
      status { 0 }
    end
    trait :status_occupied do
      status { 1 }
    end
    created_at { Time.at((Time.now + 60*60*24*365)).strftime("%Y-%m-%dT%TZ")}
    updated_at { Time.at((Time.now + 60*60*24*365)).strftime("%Y-%m-%dT%TZ")}
  end

  factory :master_model do
  	# never fill `id` it will be feed by db
  	name { Faker::Name.unique.name }
    description(:description){|n| "parking #{n}"}

    password { Faker::Alphanumeric.alpha 5 }
    cif { "B#{rand.to_s[2..11]}" }

    address { Faker::Address.street_address }
    city { Faker::Address.city }
    postal_code { Faker::Address.zip_code}

    fecha_creacion { rand.to_s[2..3].to_i.months.ago }
    fecha_modificacion { rand.to_s[2].to_i.months.ago }

    after :create do |parking|
      create :dependent_model, :status_free
      create :dependent_model, :status_occupied
      # create :parking_spot, id_parking: 4000, id_usuario: 4000
      # create :parking_spot, id_parking: parking.id, id_usuario: 4000

      create_list :dependent_model, 5, id_parking: parking.id, id_usuario: 4000


      # create :parking_spot, parking_seek_turing: 4000, status_free: 0, id_parking: 2

      # create :parking_spot, :parking_seek_turing, :status_free
      # create :parking_spot, :parking_seek_turing, :status_occupied

      # create :theme, post: post             # has_one
      # create_list :comment, 3, post: post   # has_many
    end
  end
end

```
