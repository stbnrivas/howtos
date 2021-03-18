# rake <3 



## rake task



## rake task namespace

```ruby
namespace :sdk do

end
```

## task invoking others

```ruby
  desc "all"
  task :all do
    Rake::Task["requirements:software"].execute
    Rake::Task["requirements:env"].execute
    Rake::Task["requirements:keybase_repo"].execute
    Rake::Task["requirements:aws"].execute
  end
```


## rake task with arguments

```ruby
desc "create"
task :create, [:name, :billing_group] do |task,args|
	puts args[:name]
end
```


## rake task with arguments into a rails


```ruby
desc 'level'
task :level, [:level] => :environment do |_t, args|
	abort "try `rake level[\"level\"]` with level between 0..5" if args[:level].nil? || !args[:level].to_i.is_a?(Integer)
	puts args[:level]
end
```