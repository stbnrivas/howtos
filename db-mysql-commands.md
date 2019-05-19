# mysql client

    mysql -u root -p

example for bitnami 

    mysql -u root -p --socket=/home/$user/bitnami/drupal-commerce/mysql/tmp/mysql.sock


# mysqladmin

    mysqladmin -u root -p ping
    mysqladmin -u root -p version
    mysqladmin -u root password $password
    mysqladmin -u root -p $old_password password '$new_password'


    mysqladmin -u root -p create $database
    mysqladmin -u root -p drop $database

    mysqladmin -u root -p status

    mysqladmin -u root -p reload;
    mysqladmin -u root -p refresh

    mysqladmin –help


# allow remote connections

[Inside VM]

    mysql -u root -p 
    create user developer identified by '$pass' 
    grant all privileges on *.* to developer@"%"  identified by "password";
    grant all privileges on *.* to mysql@"%"  identified by "";
    GRANT ALL ON *.* TO 'root'@'%' IDENTIFIED BY '[password]'
    flush privileges;

    /sbin/iptables -A INPUT -i eth0 -p tcp --destination-port 3306 -j ACCEPT
    /sbin/iptables -A INPUT -i eth0 -s 192.168.1.0/24 -p tcp --destination-port 3306 -j ACCEPT

    # debian based
    sudo iptables-save
    # redhat based
    service iptables save

[Outside VM]

    mysql -u developer -p --host 192.168.1.12




# PROBLEM: mysql when mysql.sock has been realocate 

    mysql -u root --socket /home/stbn/lampstack-3.0.6-0/mysql/tmp/mysql.sock


or you can find where default socket has been realocate at /etc/my.cnf

    [mysqld]
    socket=/path/to/socket
    [client]
    socket=/path/to/socket


