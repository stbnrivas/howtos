# rubocop
A ruby static code analysis tool aimed to enforce the Ruby community style guide

```bash
rubocop
rubocop --auto-gen-config
```

```bash
# search offenses full full project
rubocop

# search offenses checking specific list of files or folders
rubocop folder lib/something.rb
```


RuboCop comes with a preconfigured set of rules for each of its cops you may wish to reconfigure a cop, tell to ignore certain files, or disable it altogether.

The most common way to change RuboCop’s behaviour is to create a configuration file named .rubocop.yml in the project’s root directory.



```bash
bundle add rubocop-rails
```


```yml
# .rubocop.yml
require: rubocop-rails
```
