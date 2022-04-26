## ubuntu 18.04 LTS 版本安裝
1. 建立 vm instance
2. 搜尋 vpc network，將`外部IP位址`變更為`靜態`，以免造成IP因停機後變更。
<br/>

<br/>


## 配置檔文件位置
* php.ini 配置文件使用 `php -i | grep php.ini` 尋找。
* PHP FPM 配置文件在 `/etc/php/7.4/fpm/pool.d/www.conf`。  
* mysql 配置檔位置 `/etc/my.cnf` 或 `/etc/mysql/my.cnf`。


<br/>

<Br/>

## 安裝php, php套件
ubuntu 14.04 預設 php5.6；ubuntu 16.04 預設 php7.0；如果要安裝其他 php版本只能依靠第三方庫，`ppa:ondrej/php`是較有名的第三方庫。
```sh
sudo apt-get update
# 為 add-apt-repository 的依賴套件
# -y 安裝時全部yes
sudo apt -y install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt -y install php7.4
php -v
```
```sh
# 安裝套件
sudo apt-get install -y php7.4-{bcmath,bz2,intl,gd,mbstring,mysql,zip,common}

sudo apt install php7.4-fpm php7.4-intl php7.4-imap php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-cli php7.4-zip curl

```

<br/>

<br/>

## 安裝 nginx
```sh
# 查看當前正在監聽的 port
sudo lsof -i -n -P|grep LISTEN

# 停用apache
sudo systemctl disable --now apache2

# 安裝nginx php fpm
sudo apt-get install nginx php7.4-fpm

# 檢查 php-fpm nginx 是否運行
systemctl status php7.4-fpm nginx
```

<br/>

<br/>

## 安裝 npm
```sh
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt install nodejs

node -v
```

<br/>

<br/>

## 安裝 mysql
```sh
sudo apt install mysql-server
```

(補充)修改 root 密碼
```sql
-- 查看: 如果 root 的plugun是 auth_socket，會無法改root密碼
USE mysql;

SELECT User, Host, plugin FROM mysql.user;

+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| root             | auth_socket           |
| mysql.sys        | mysql_native_password |
| debian-sys-maint | mysql_native_password |
+------------------+-----------------------+
```
```sql
-- 修改 root 密碼
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'new-password';

FLUSH PRIVILEGES;

exit;

sudo service mysql restart
```

<br/>

<br/>

## laravel 擴充套件
```sh
sudo apt install composer
sudo apt-get install php7.4-gmp
sudo apt-get install php7.4-xml
sudo apt-get install php7.4-curl
```

## 設定時區
```sh
sudo timedatectl set-timezone Asia/Taipei
```

<br/>

<br/>

## nginx 設定
```sh
sudo vim /etc/nginx/sites-available/laravel.conf
```
需把大括號拿掉
```sh
server {
    listen 80;
    server_name {example.com}; 
    root {/var/www/html/MyProject/public};

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

`sites-enabled/laravel.conf` 軟連結會指向 `sites-available/laravel.conf` 的檔案位置。
```sh
sudo ln -s /etc/nginx/sites-available/laravel.conf /etc/nginx/sites-enabled/
```
把`sites-enabled`和`sites-available`下的 default 檔案都刪除。
```sh
sudo rm /etc/nginx/sites-enabled/default
sudo rm /etc/nginx/sites-available/default
```
調整權限
```sh
sudo chown -R www-data:www-data /var/www/MyProject/
sudo chmod -R 755 /var/www/MyProject/
sudo chmod -R 755 storage
sudo chmod -R 755 bootstrap/cache
```
重開 nginx
```sh
sudo systemctl reload nginx
sudo systemctl restart nginx
```
laravel 配置
```sh
# 將登入帳號加到www-data權限
sudo useradd -g www-data ricoliang0214
composer install
sudo npm install
sudo npm run dev
php artisan key:generate
cp .env.example .env
```