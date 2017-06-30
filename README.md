## arch linux php5.6 with mariadb

### update system

    - sudo pacman -Syu

### set permissions

    if you do not set permissions you wont be able to edit/create any files in our apache dir

    create own group first, then you will follow the instructions so on. replace /var/www with /srv/http

    https://superuser.com/questions/19318/how-can-i-give-write-access-of-a-folder-to-all-users-in-linux

### Install Apache

    - sudo pacman -S apache

    sudo systemctl enable httpd
    sudo systemctl restart httpd
    sudo systemctl status httpd (should see that it's active, any changes to httpd must be met with a restart to see changes)

    you can navigate to localhost or 127.0.0.1 and see some structure.

### Install MariaDB(same as mysql)

    - sudo pacman -S mysql

    sudo systemctl enable mysqld
    sudo systemctl start mysqld
    sudo systemctl status mysqld

    **set up root user**

    sudo mysql_secure_installation

### Install PHP & PHP Apache

    sudo pacman -S php-apache

    https://aur.archlinux.org/pkgbase/php56/?comments=all
    extract it how you like and

    makepkg -s

    - replace /etc/httpd/conf/httpd.conf with httpd.conf from this repo

    **make an info php**

    sudo vim /srv/http/test.php

    <?php phpinfo();

    sudo systemctl restart httpd

### Install PHPmyadmin

    sudo pacman -S phpmyadmin php-mcrypt

    replace etc/php56/php.ini with the one from the repo

    sudo vim /etc/httpd/conf/extra/phpmyadmin.conf

    Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
    <Directory "/usr/share/webapps/phpMyAdmin">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
    </Directory>

sudo systemctl restart httpd
sudo systemctl restart mariadb
