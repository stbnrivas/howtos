
```ruby
# Dir.glob("**/*/") # for directories
# Dir.glob("**/*") # for all files

Dir.glob("**/run/media/stbn/*") do |f|
  put f
end # for directories

Dir.glob('/run/media/stbn/Nuevo vol/RESTORED/*.jpg') do |file|
 puts file
end

```
