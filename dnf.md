# dnf commons

	dnf search <package>
	dnf install <package>
	dnf remove <package>	
	dnf update
	
# list packages installed

	dnf list installed | grep <package>
	
# add repo | disabled repo

	dnf config-manager --add-repo repository_url
	dnf config-manager --set-disabled repository…

# show files with path of package installation

	dnf repoquery -l <package>

# rpm 

## installation from rpm
rpm -ihv --force <packagename>

## use following syntax to list the files for already INSTALLED package:
rpm -ql package-name

## use following syntax to list the files for RPM package:
rpm -qlp package.rpm
