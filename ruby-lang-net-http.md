# ruby Net:HTTP


```
require 'net/http'
# no more dependence to require 'uri'
```


- get 

```bash
req = Net::HTTP::Get.new(cb_uri.path)
req["X-Auth-Token"] = token
req["Fiware-Service"] = $config.fiware_service if $config.fiware_service_enable?
# ap "============="
# ap req.to_hash
# ap cb_uri
# ap request.methods - Object.methods
# ap "=============1"
req.each_header do |h|
ap h
end
response = Net::HTTP.start(cb_uri.host,cb_uri.port) do |http|
# ap "=============2"
http.request(req)
end
response.each_header do |h|
ap h
end

ap response.class
ap response.code
ap response.body
ap response.to_hash


```

- post

- put

- patch

- delete


# all object http has

request and response are http objects

each_header do |h|

end

request.body...



- working with a session

session http are expensive reuse that







backoff with requests...

```ruby
require "net/http"
require "uri"
url = URI.parse("http://www.whatismyip.com/automation/n09230945.asp")
req = Net::HTTP::Get.new(url.path) 
req.add_field("X-Forwarded-For", "0.0.0.0") 
res = Net::HTTP.new(url.host, url.port).start do |http| 
	http.request(req) 
end puts 
res.body
```




    [ 0]                       [](?) ?
    [ 1]                      []=(?) ?
    [ 2]                add_field(?) ?
    [ 3]               basic_auth(?) ?
    [ 4]                     body(?) ?
    [ 5]                    body=(?) ?
    [ 6]              body_exist?(?) ?
    [ 7]              body_stream(?) ?
    [ 8]             body_stream=(?) ?
    [ 9]           canonical_each(?) ?
    [10]                 chunked?(?) ?
    [11]        connection_close?(?) ?
    [12]   connection_keep_alive?(?) ?
    [13]           content_length(?) ?
    [14]          content_length=(?) ?
    [15]            content_range(?) ?
    [16]             content_type(?) ?
    [17]            content_type=(?) ?
    [18]           decode_content(?) ?
    [19]                   delete(?) ?
    [20]                     each(?) ?
    [21]         each_capitalized(?) ?
    [22]    each_capitalized_name(?) ?
    [23]              each_header(?) ?
    [24]                 each_key(?) ?
    [25]                each_name(?) ?
    [26]               each_value(?) ?
    [27]                     exec(?) ?
    [28]                    fetch(?) ?
    [29]               form_data=(?) ?
    [30]               get_fields(?) ?
    [31]   initialize_http_header(?) ?
    [32]                     key?(?) ?
    [33]                   length(?) ?
    [34]                main_type(?) ?
    [35]                     path(?) ?
    [36]         proxy_basic_auth(?) ?
    [37]                    range(?) ?
    [38]                   range=(?) ?
    [39]             range_length(?) ?
    [40]  request_body_permitted?(?) ?
    [41] response_body_permitted?(?) ?
    [42]        set_body_internal(?) ?
    [43]         set_content_type(?) ?
    [44]                 set_form(?) ?
    [45]            set_form_data(?) ?
    [46]                set_range(?) ?
    [47]                     size(?) ?
    [48]                 sub_type(?) ?
    [49]                  to_hash(?) ?
    [50]              type_params(?) ?
    [51]               update_uri(?) ?
    [52]                      uri(?) ?
]
