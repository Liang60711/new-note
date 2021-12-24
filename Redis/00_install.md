# 安裝 Redis
1. 在 Mac 環境下載

    ```sh
    brew install redis
    ```

2. 開啟/確認 redis-server

    ```sh
    redis-server
    ```

3. 另外開啟一個 TTY，進入 redis-cli，(因為redis-server不是detach在背景執行)

    ```sh
    redis-cli
    ```
4. 安裝browser：`Anthor Redis Desktop Manager`
    
    ```sh
    brew install --cask another-redis-desktop-manager
    ```

    進入此App前，需在Mac的安全與隱私權允許，可以檢查key,value是否存在db0。

    ```sh
    # 在 redis-cli中測試
    >> set foo bar

    >> get foo
    ```

5. 下載 phpredis API

    ```sh
    # 支援 php5.6 的最高版本，若是php>=7可以使用其他安裝方式
    pecl install redis-2.2.8
    ```
    並在 `php.ini` 中加入

    ```conf
    extension=redis.so
    ```
    檢查：網頁連結至 `phpinfo.php`，查看 redis 版本。

    