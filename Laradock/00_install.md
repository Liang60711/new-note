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
