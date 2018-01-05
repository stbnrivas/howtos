# user management

    $ useradd newuser
    $ userdel newuser

# group management

$ groupadd newgroup
$ groupdel newgroup


# adding user to a group

	$ usermod -a -G newgroup newuser

-a option, for append, so as to avoid removing already existing groups

# removing group 

	$ usermod -G newgroup newuser


can check if it works with

	$ groups


