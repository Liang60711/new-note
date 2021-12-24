# Connect to redis server

建立 instance，並建立連線
```php
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);
```