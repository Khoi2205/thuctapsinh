```
#!/bin/bash 

# Check OS
cat /etc/os-release* |grep 'ubuntu' > /dev/null 2>&1 && OS='Ubuntu'
cat /etc/os-release* |grep 'centos' > /dev/null 2>&1 && OS='CentOS' 
echo $OS

if [ -d /var/lib/mysql ]
then
    yum -y remove mariadb mariadb-server 
    rm -rf /var/lib/mysql  
fi

yum -y install httpd
systemctl start httpd.service
systemctl enable httpd.service
yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum -y install epel-release yum-utils
yum-config-manager --disable remi-php54
yum-config-manager --enable remi-php73
yum -y install php php-cli php-fpm php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json
php -v
systemctl restart httpd
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*
yum -y install epel-release
yum -y install mariadb-server mariadb
systemctl start mariadb.service
systemctl enable mariadb.service

config_wp(){
    cd ~ && mkdir wp-down
    cd wp-down
    wget http://wordpress.org/latest.tar.gz
    tar xvfz latest.tar.gz
    rm -rf  /var/www/html/*
    cp -Rvf ~/wp-down/wordpress/* /var/www/html
    cd /var/www/html
    cp wp-config-sample.php wp-config.php
    sed -i -e "s/database_name_here/"$databasename"/g; s/username_here/"$username"/g; s/password_here/"$userpassword"/g; s/localhost/$host/g  " /var/www/html/wp-config.php
    chmod -R 755 /var/www/*
    chown -R apache:apache /var/www/*
    systemctl restart httpd
}
install_mariadb(){
    echo -e "\ny\n$mysqlRootPass\n$mysqlRootPass\ny\ny\ny\ny\ny\n" |mysql_secure_installation --stdin
    mysql -u root -p$mysqlRootPass<<EOF 
    CREATE DATABASE $databasename;
    CREATE USER $username@$host IDENTIFIED BY '$userpassword';
    GRANT ALL PRIVILEGES ON $databasename.* TO $username@$host IDENTIFIED BY '$userpassword';
    FLUSH PRIVILEGES;
    exit
EOF
}
# install_mariadb

if [ "$OS"="CentOS" ]
then     
    read -p "Nhập mật khẩu cho mysqlroot: " mysqlRootPass
    read -p "Nhập tên cho Database: " databasename
    read -p "Nhập Database username: " username
    read -p "Nhập Database password username: " userpassword
    read -p "Nhập MatiaDB host: (Enter for localhost):" host

    if [ "$host" = "" ]
    then 
    host="localhost"
    fi
    set -e
    yum install -y wget > /dev/null 2>&1
    config_wp
    install_mariadb  
    firewall-cmd --zone=public --add-port=80/tcp --permanent > /dev/null 2>&1
    firewall-cmd --reload > /dev/null 2>&1
    systemctl reload httpd
fi
```