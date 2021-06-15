# bash

## 特性
保存執行過的命令，每個 user 是分開的檔案
```sh
history
```
自定義 history 功能，可更改環境變數。
* <code>$HISTSIZE</code>: 記憶體中保存的數量。
* <code>$HISTFILE</code>: 歷史檔案位置。
* <code>$HISTFILESIZE</code>: 歷史檔案中保存的數量 (關機時會將記憶體中的指令存成檔案)。

    ```sh
    # 查看環境變數
    echo $HISTFILESIZE

    # 刪除記憶體中所有 history
    history -c

    # 刪除指定 history 304行
    history -d 304

    # 將目前記憶體中紀錄，存到歷史檔案
    history -w

    # 從歷史檔案讀取紀錄
    history -r

    # 使用最近一個以 m 開頭的指令 (常用)
    history !m
    ```
