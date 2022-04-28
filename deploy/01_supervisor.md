## 安裝 supervisor
```sh
sudo apt install supervisor
```
安裝後進入設定資料夾
```sh
cd /etc/supervisor
vim supervisord.conf
```
此檔案會 include 以下位置檔案，要注意不同系統，副檔名不一樣 
* CentOS - ini
* Ubuntu - conf
```php
[include]
files = /etc/supervisor/conf.d/*.conf
```
之後在 conf.d 底下建立 config 檔案
```sh
vim /etc/supervisor/conf.d/{laravel-work}.conf
```

```conf
[program:worker-command]
process_name=%(program_name)s_%(process_num)02d
# queue:work指令
command=php /var/www/html/digiwin-api/artisan queue:work digiwinapi --queue=commands --sleep=1 --tries=3
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=1
redirect_stderr=true
# log file位置可放在專案中
stdout_logfile=/var/www/html/digiwin-api/storage/logs/worker.log
stopwaitsecs=3600

[program:worker-scanner]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/html/digiwin-api/artisan queue:work digiwinapi --queue=scanners
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=4
redirect_stderr=true
stdout_logfile=/var/www/html/digiwin-api/storage/logs/worker-scanner.log
stopwaitsecs=3600
```
修改檔案執行權
```sh
chmod -R +x /etc/supervisor/conf.d
```
啟動 supervisord
```sh
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start laravel-worker:*
```
每次程式更新後，執行
```sh
sudo supervisorctl restart all
```
停止運行
```sh
sudo supervisorctl stop {laravel-worker}:*
```

<br/>

<br/>