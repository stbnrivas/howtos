# rubygems commands cheatsheet



## help

	gem help install						show the help of install
	gem help examples						show the example of gem

## creation of ruby gems

	bundle gem gem_name						creating ruby gems

	gem -v									gem version
	gem build *.gemspec						Build a gem
	gem install *.gem          	   			Install locally
	gem environment							show the environment of gem
	cd $(basename `gem which rake`)			Go to a gem's path

	gem update								update all gempackage
	gem update --system						update RubyGems


## listing and searching gems

	gem list								List local gems
	gem list -r								List remote gems
	gem which rake							Point to where lib/rake.rb is
	gem search -r <gem>						remote search for gems

	gem list <gem> --remote --all			search all versions of gems
	gem search --remote --all | grep "^rails"


## installation 

	gem install <gem>						install last version
	gem install <gem> -v 2.3				install the specific version
	gem install <gem> -v "=2.3.0"
	gem install <gem> --version "=2.3.0"

	gem lock								generate a lockdown list of gems

	gem build rake.gemspec					compile rake.gemspec into rake.gem

	gem dependency rails -v 0.10.1			show thr list of packages depandent on rails


## uninstallation

	gem cleanup <gem>						remove all old versions of the gem

	gem uninstall <gem>						choose which ones you want to remove
	gem uninstall <gem> --version 1.1.9		remove version 1.1.9 only
	gem uninstall <gem> --version '<1.3.4'	remove all versions less than 1.3.4
	gem cleanup --dryrun					for removing older versions of all installed gems, with preview what gems are going to be removed.
	
	gem uninstall --all 					to remove all
	gem cleanup 							removing older versions

	gem list | cut -d” ” -f1 | xargs gem uninstall -aIx   remove all gem


## rubygems.org 

	gem push *.gem							Upload to rubygems.org
	gem yank foogem -v 0.0.1				Take it back
	gem owner foogem --add <another-owner-to-add@gem.com>




















