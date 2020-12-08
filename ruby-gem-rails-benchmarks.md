
# optimizar las queries en rails


gem annotate       anota los campos del modelo en
gem bullet para eliminar  n+1 queries

materialized view


- User
  + id
  + name
  + role

- Song
  + id
  + title
  + duration
  + progress

- Ratings
  + id
  + ratingable_type
  + ratingable_id
  + user_id
  + value

- Album
  + id
  + title

- Artist
  + id
  + name
  + age


el rate mas alto de los albums

```ruby
Album.joins(:ratings).map{ |album| album.ratings.length}.max

#
# select albums.* from albums
# inner join "ratings" on ratings.ratingable_id = albums.id AND ratings.ratingable_type = 'Album'


Album.include(:ratings).map{ |album| album.ratings.lenth}.max

# select albums.* from albums
#
# select ratings.* from albums
# where "ratings".ratingable_type = "Album" AND ratings.ratingable_id IN (1,2,3,4,5,6,7,8,9,...)
#
```

usamos un modulo de ruby llamado benchmark

```ruby
Benchmark.bm do |x|
	x.report { Albums.joins(:ratings).map { |album| album.ratings.lenght}.max }
	x.report { Albums.includes(:ratings).map { |album| album.ratings.lenght}.max }
end

# 19s
# 0.5s
```

```ruby
Benchmark.bm do |x|
	x.report { Albums.joins(:ratings).map { |album| album.ratings.count}.max }
	x.report { Albums.includes(:ratings).map { |album| album.ratings.count}.max }

end

# 11
#  1.5
```

con demasidos registros usa metodos de ruby: no uses joins

CUANDO USAR JOINS

usa joins cuando necesitamos hacer una condicion

```
Album.joins(:ratings).where("ratings.value > ?", 3).pluck(:title)
```

```ruby
Benchmark.bm do |x|
	x.report { Album.joins(:ratings).where("ratings.value > ?",3).pluck(:title) }
	x.report { Album.includes(:ratings).joins(:rating).where("ratings.value > ?",3).pluck(:title)}
end

#0.7s
# 0.7s

```




