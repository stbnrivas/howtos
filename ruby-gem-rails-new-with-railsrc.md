# rails new customize using railsrc

using railsrc you dont have to remember all flags even you can set specific flags

```bash
touch .railsrc
```


rails new search for `.railsrc` to use or if don't exist use the defaul behaviour:

```
# .railsrc
--database=postgresql
--api
--skip-test
--skip-bundle
--skip-spring
```

In addition you can use a rails template

```
# .railsrc
--database=postgresql
--api
--skip-test
--skip-bundle
--skip-spring
--template=~/railscustom/rails-template.rb
```










