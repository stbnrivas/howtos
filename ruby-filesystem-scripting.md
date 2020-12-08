# ruby file system scripting


1. list folder files/folder

```ruby
Dir.foreach('/run/media/user/Nuevo vol/RESTORED') do |item|
  next if item == '.' or item == '..'
  # do work on real items
  puts item
end
```


2. list folders or files only

```ruby
# Dir.glob("**/*/") # for directories
# Dir.glob("**/*") # for all files

Dir.glob("**/run/media/user/*") do |folder|
  put folder
end

Dir.glob('/run/media/user/Nuevo vol/RESTORED/*.jpg') do |file|
 puts file
end
```


3. a renamer to add a '0' as prefix


```ruby
require 'fileutils'

Dir["./*.mp3"].each do |f|
	#puts f if f.length == 19
	# puts f if f.to_s.length == 20
	if f.to_s.length == 20
		src = f.dup
		dst = f.dup
		dst.insert(14,'0')
		puts "mv #{src} #{dst}"
		FileUtils.mv(src, dst)
	end
end
```



4. renamer prefixer with left padding

```ruby
#input_dir = "/path"
#Dir.chdir(input_dir)
#search_string = input_dir + "/*.rb"
#ruby_files = Dir[search_string]
#ruby_files.each do |file|
#  system("ruby", file)
#end


$padding = 3
$path = "."

Dir["./*.mp4","./*.vtt"].each do |f|
	puts "mv '#{f}' \n" 
	puts "-"
	#system("mv #{}", file)
end
```