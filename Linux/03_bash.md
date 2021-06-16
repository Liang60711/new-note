# bash

## history
保存執行過的命令，每個 user 是分開的檔案
```sh
history
```
自定義 history 功能，可更改環境變數。
* <code>$HISTSIZE</code>: 記憶體中保存的數量。
* <code>$HISTFILE</code>: 歷史檔案位置。
* <code>$HISTFILESIZE</code>: 歷史檔案中保存的數量 (關機時會將記憶體中的指令存成檔案)。
* <code>$HISTCONTROL</code>: 紀錄環境變數，分為: 
    * <code>ignoredups</code>: 忽略連續的指令，只會紀錄一筆
    * <code>ignorespace</code>: 忽略以空白字串開頭的指令
    * <code>ignoreboth</code>: 同時啟用

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
修改變數的值，只對當前 shell 有效
```sh
# VAR_NAME="VALUE"，不用加$號
# 1
HISTCONTROL=ignoreboth

# 2
HISTSIZE=1001
```


(常用指令)使用上一個命令的最後一個參數: 
1. 快捷鍵形式: <code>ESC</code> 再按 <code>.</code>。
2. 字串形式: <code>!$</code>

<br/>

## 命令補全機制
* 查找機制: 根據 $PATH 環境變數設定的路徑，由左至右查找。
* 補全機制: 若命令符合唯一選項，按一次 tab 鍵可直接補全；若按第二次，會列出所有列表提供選則。


## 路徑補全機制
* 補全機制: 在給定的路徑下，若路徑符合唯一選項，按一次 tab 鍵可直接補全；若按第二次，會列出所有列表提供選則。


## 命令行展開
* <code>~</code>: 自動展開為用戶的家目錄，或指定用戶的家目錄。
* <code>{}</code>: 可裝入一個以逗點分隔的路徑列表，並能夠展開為多個路徑；如: <code>/tmp/{a,b}</code> 等於 <code>/tmp/a</code> 和 <code>/tmp/b</code>

```sh
# 如何同時建立 4 個目錄
# /tmp/x/y1
# /tmp/x/y2
# /tmp/x/y1/a
# /tmp/x/y1/b

mkdir -pv /tmp/x/{y1/{a,b},y2}
```
```sh
# 如何同時建立 4 個目錄
# /tmp/a_c
# /tmp/a_d
# /tmp/b_c
# /tmp/b_d

mkdir -v /tmp/{a,b}_{c,d}
```
```sh
# 建立以下路徑
# /tmp/mysysroot
# ├── bin
# ├── etc
# │   └── sysconfig
# │       └── network-scripts
# ├── sbin
# ├── usr
# │   ├── bin
# │   ├── lib
# │   ├── lib64
# │   ├── local
# │   │   ├── bin
# │   │   ├── etc
# │   │   ├── lib
# │   │   └── sbin
# │   └── sbin
# └── var
#     ├── cache
#     ├── log
#     └── run

mkdir -pv /tmp/mysysroot/{bin,sbin,etc/sysconfig/network-scripts,usr/{bin,sbin,lib,lib64,local/{bin,etc,lib,sbin}},var/{cache,log,run}}
```

## 命令執行結果狀態碼
可使用 <code>$?</code> 來回報上一個命令的結果:
* 成功: 0
* 失敗: 1-255

## 引用命令執行結果 (常用)
```sh
# 將指令的結果存成變數 (兩種皆可)
$(COMMAND)
`COMMAND`

# 將現在時間存成資料夾名稱
mkdir $(date +%H:%M:%S)
```

## 引用
* 強引用: ''
* 弱引用: ""
* 命令引用: ``

## 快捷鍵
* <code>ctrl+a</code>: 跳至命令行字首 
* <code>ctrl+e</code>: 跳至命令行字尾
* <code>ctrl+u</code>: 刪除命令行字首到游標處
* <code>ctrl+k</code>: 刪除命令行游標處到字尾
* <code>ctrl+l</code>: 同命令 <code>clear</code>