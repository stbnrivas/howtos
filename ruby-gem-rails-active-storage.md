# active storage

[https://edgeguides.rubyonrails.org/active_storage_overview.html](https://edgeguides.rubyonrails.org/active_storage_overview.html)


new tables `active_storage_blobs` `active_storage_attachments`


```bash
bin/rails active_storage:install
bin/rails db:migrate
```


```ruby
# app/models/user.rb
class User < ApplicationRecord
	has_one_attached :image
	has_many_attached :uploads
end
```

```ruby
class PublicController < ApplicationController

# ...
private
  def post_params
  	params.permit(:post).permit(:image, :uploads)
  end
end
```


```ruby
# config/environments/{development,production,test}.rb

config.active_storage_.service = :local
```

```yml
# config/storage.yml
local:
  service: Disk
  root: <%= Rails.root.join("storage") %>
  # host: "http://localhost:5000"

digitalocean:
  service: S3
  access_key_id: <%= Rails.application.creadentials.dig%>
  secret_access_key:
  region: myc3
  bucket: gorails
  endpoint: 'https://'
```


```bash
bin/rails generate model Document name
```


```erb
<%= form_with(model: post, local: true) do |form| %>
<div class="form-group">
	<%= form.label :single_upload %>
	<%= from.file_field :image, class:"form-control" %>
</div>

<div class="form-group">
	<%= form.label :multiple_upload %>
	<%= form.file_field :uploads, multiple: true, class:"form-control" %>
</div>
<% end %>
```


```erb
<%= link_to image_tag(upload.preview(resize: "400x400")), upload %>
<%= link_to image_tag(upload.preview(resize: "400x400")), rails_blob_path(upload, disposition: :attachment) %>
```
