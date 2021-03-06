# Requirements
* git
* docker [ >= 17.12 ]

<br/>

<br/>

# Installation
## 已有單一 project
1. 將laradock下載至專案目錄內`git submodule add https://github.com/Laradock/laradock.git`

2. 目錄結構 
```
.
└──project-a
   └──laradock-a
```

## 尚未建立單一 project(用法同上)
1. 下載 laradock 平行於專案目錄 `git clone https://github.com/laradock/laradock.git`
2. 目錄結構
```
.
|──project-z
└──laradock
```
3. 新增 `.env` 檔案
```
cd laradock
cp .env.example .env
```

4. 修改 `.env` 檔案
```sh
# 將此路徑設定為 laradock workspace 的根目錄
APP_CODE_PATH_HOST=../project-z/

# 在 docker (linux) 中的 workspace 目錄
APP_CODE_PATH_CONTAINER=/var/www

# 資料庫儲存資料的目錄
DATA_PATH_HOST=~/.laradock/data
```

5. run container
nginx 和 apache 都依賴 `php-fpm`，因此會自動下載並開啟
```
docker-compose up -d nginx mysql
```

6. 在 workspace 內使用 bash
```
docker-compose exec workspace bash
```

7. `.env` 環境設置
```sh
### laradock .env 
### MYSQL #################################################
DB_HOST=mysql
MYSQL_VERSION=8.0
MYSQL_DATABASE=default
MYSQL_USER=root
MYSQL_PASSWORD=
MYSQL_PORT=3306
MYSQL_ROOT_PASSWORD=root
MYSQL_ENTRYPOINT_INITDB=./mysql/docker-entrypoint-initdb.d


### laravel project .env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=default
DB_USERNAME=root
DB_PASSWORD=root
```

<br/>

<br/>

# 切換成 php5.6 版本

1. 修改 `.env` 
```
PHP_VERSION=5.6
```

2. 下指令 rebuild the image
```
docker-compose build php-fpm
```

3. 重開 docker-compose
```
docker-compose down 
docker-compose up -d nginx mysql
```

<br/>

<br/>

# mysql 若無法在 M1 使用
在 `docker-compose.yml` 新增
```yml
image: mysql:8.0.19
platform: 'linux/x86_64'
```

<br/>

<br/>

# 將 mysql 切換成 mariadb
mysql 當前無法使用在 M1 上，需要更換成 mariadb，需修改 `.env`
```sh 
# 需新增
DB_HOST=mariadb
# 需修改
PMA_DB_ENGINE=mariadb
```
在 `localhost:8081` 開啟 phpmyadmin (admin / common user)
* server: mariadb
* username: root/default 
* password: root/secret
