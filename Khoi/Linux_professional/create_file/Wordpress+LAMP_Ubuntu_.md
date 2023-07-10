```
#!/bin/bash

# Check OS
cat /etc/os-release* | grep 'ubuntu' > /dev/null 2>&1 && OS='Ubuntu'
cat /etc/os-release* | grep 'centos' > /dev/null 2>&1 && OS='CentOS'
echo $OS

if [ "$OS" = "Ubuntu" ]; then
    if [ -d /var/lib/mysql ]; then
        apt-get remove --purge mariadb-* -y
        rm -rf /var/lib/mysql
    fi

    Install_Ubuntu() {
        apt-get update
        apt-get install -y apache2 php libapache2-mod-php mariadb-server php-mysql php-gd
        systemctl start apache2
        systemctl enable apache2
        systemctl start mariadb
        systemctl enable mariadb
    }

    config_wp() {
        cd ~ && mkdir wp-down
        cd wp-down
        wget http://wordpress.org/latest.tar.gz
        tar xvfz latest.tar.gz
        rm -rf /var/www/html/*
        cp -Rvf ~/wp-down/wordpress/* /var/www/html
        cd /var/www/html
        cp wp-config-sample.php wp-config.php
        sed -i -e "s/database_name_here/$databasename/g; s/username_here/$username/g; s/password_here/$userpassword/g; s/localhost/$host/g" /var/www/html/wp-config.php
        chmod -R 755 /var/www/*
        chown -R www-data:www-data /var/www/*
        systemctl restart apache2
    }

   install_mariadb(){
    echo -e "\ny\n$mysqlRootPass\n$mysqlRootPass\ny\ny\ny\ny\ny\n" | mysql_secure_installation

    mysql -u root -p$mysqlRootPass <<EOF
    CREATE DATABASE $databasename;
    CREATE USER '$username'@'$host' IDENTIFIED BY '$userpassword';
    GRANT ALL PRIVILEGES ON $databasename.* TO '$username'@'$host';
    FLUSH PRIVILEGES;
    exit
EOF
}

    read -p "Enter the MySQL root password: " mysqlRootPass
    read -p "Enter the database name: " databasename
    read -p "Enter the username: " username
    read -p "Enter the user password: " userpassword
    read -p "Enter the MariaDB host (Enter for localhost): " host

    if [ "$host" = "" ]; then
        host="localhost"
    fi

    set -e
    apt-get install -y wget > /dev/null 2>&1
    Install_Ubuntu
    config_wp
    install_mariadb
    ufw allow 'Apache'
    systemctl restart apache2
fi
```