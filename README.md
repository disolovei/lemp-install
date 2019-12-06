# On Ubuntu 18.04

## 1. Preparing

```shell script
sudo apt update
```

```shell script
sudo apt upgrade
```

## 2. Nginx

[Link RU](https://www.digitalocean.com/community/tutorials/nginx-ubuntu-18-04-ru)

```shell script
sudo apt install nginx
```

### 2.1 Commands

```shell script
systemctl status nginx
```

```shell script
sudo systemctl stop nginx
```

```shell script
sudo systemctl start nginx
```

```shell script
sudo systemctl reload nginx
```

```shell script
sudo systemctl restart nginx
```

```shell script
sudo systemctl disable nginx
```

```shell script
sudo systemctl enable nginx
```

### 2.2 WordPress Server Block config simple example

#### 2.2.1 Create server blog config file

```shell script
sudo nano /etc/nginx/sites-available/example.loc
```

#### 2.2.2 Put to config file

```
server {
	listen 80;

	server_name example.loc;

	root /var/www/example.loc/public_html;

	index index.php index.html;

	location / {
		try_files $uri $uri/ /index.php?$args;
		autoindex on;
	}

	location ~ \.php$ {
		include /etc/nginx/fastcgi_params;
		try_files $uri =404;
		include /etc/nginx/fastcgi.conf;
		fastcgi_pass unix:/run/php/php7.2-fpm.sock;
	}
}

```

#### 2.2.2 Server block activation

```shell script
sudo ln -s /etc//nginx/sites-available/example.loc /etc/nginx/modules-enabled/example.loc
```

#### 2.2.3 Open hosts file

```shell script
sudo nano /etc/hosts
```

#### 2.2.4 Add new line to hosts

```
127.0.0.1   example.loc
```

### 2.3 Change server block folder owner (edit files allowed)

```shell script
sudo usermod -a -G www-data your_user
```

```shell script
sudo chgrp -R www-data /var/www/example.loc/public_html
```

```shell script
sudo chmod -R g+w /var/www/example.loc/public_html
```

## 3. MySQL (MariaDB)

[Link EN](https://www.digitalocean.com/community/tutorials/mysql-ubuntu-18-04-ru)

```shell script
sudo apt install mysql-server
```

### 3.1 Add new MySQL user

```mysql
CREATE USER '$username'@'localhost' IDENTIFIED BY '$user_password';
```

```mysql
GRANT ALL PRIVILEGES ON *.* TO '$username'@'localhost' WITH GRANT OPTION;
```

```shell script
exit
```

## 4. PHP

[Link EN](https://thishosting.rocks/install-php-on-ubuntu/)

### 4.1. PHP 7.2

```shell script
sudo apt install php
```

```shell script
php -v
```

```shell script
sudo apt install php-pear php-fpm php-dev php-zip php-curl php-xmlrpc php-gd php-mysql php-mbstring php-xml libapache2-mod-php
```

## 5. PhpMyAdmin

[Link EN](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-18-04-server)

```shell script
sudo apt install phpmyadmin
```

```shell script
sudo ln -s /usr/share/phpmyadmin /var/www/path_to_folder
```

```shell script
https://server_domain_or_IP/phpmyadmin
```

