# 檔案與目錄管理
## ls
```sh
ls -l           # 顯示詳細資料
ls -a           # 顯示隱藏檔 (以"."開頭的檔案)
ls -h           # 做單位轉換
ls -d           # 只顯示目錄
ls -i           # 顯示 inode (index node)
ls -r           # 反向排序文件
ls -R           # 遞迴列出所有子目錄的檔案
ls -al|more     # 將檔案內容以一頁一頁顯示
ls -ltr         # 檔案依照時間排序，讓最新的檔案排在最後
```

## pwd
```sh
pwd             # 顯示當前路徑
```

## cd
```sh
cd              # 家目錄
cd ~            # 家目錄 (同上)
cd -            # 往返目錄 (遙控器上的返回鍵)
```

## more
```sh
more .bashrc    # 查看 .bashrc 檔案，一頁一頁看
```


## mkdir
```sh
mkdir test      # 建立 test 目錄
```


## rmdir
```sh
mkdir test      # 移除 test 目錄，如果內有檔案無法刪除
```
## rm -rf
```sh
rm -rf test     # 強制刪除
```

## mv
<code>mv <來源目錄或檔案> <目的目錄></code>
```sh
mv .bashrc /    # 將 .bashrc 檔案移至根目錄
mv /.bashrc .   # 將 /.bashrc 移至目前目錄
```

## cp
<code>cp <來源檔案> <目的檔案></code>
```sh
cp .bashrc /home
```

## ln
連結 (link) 可以視為檔案的別名，分為:
* 軟連結 (symbolic link):
    1. 以路徑型式存在，類似 windows 捷徑。 
    2. 可跨越檔案系統。
    3. 可對一個不存在的檔案進行連結。
    4. 可對目錄進行連結。
* 硬連結 (hard link):  
    1. 以檔案副本型式存在，但不占用實際空間。
    2. 不可跨越檔案系統。
    3. 不可對目錄進行連結。
    4. ln 指令預設使用應連結。
    5. 刪除副本檔案會造成原檔案也跟著刪除。

<code>ln -s <來源檔案(目錄)> <目的檔案(目錄)></code>
```sh
ln -s /usr/bin bin      # -s 為建立 symbolic 連結
```

## find 
搜尋檔案，可以指定範圍。  
<code>find <路徑> -name <檔名></code>
```sh
find / -name bin        # 在跟目錄中尋找名稱為 bin 的檔案
```

## whereis
搜尋檔案，利用曾經找過的系統內的資訊找檔案，速度較快，找不到並不代表不存在。
```sh
whereis bin
```

## df
查看硬碟空間
```sh
df
```

## du
查看目錄內所有檔案使用的硬碟空間
```sh
du
```

<br/>

<br/>

# 系統管理

## type
顯示命令類型
```sh
type su
```

## su
進入 super user 模式，需要輸入 root 密碼。
```sh
su
```
設定 root 密碼
```sh
sudo passwd root
```

## passwd
更改登入密碼
```sh
passwd
```

## who
查看系統上的使用者。  
<code>who</code> 和 <code> w</code> 功能基本相同，<code>who</code> 僅列出 user 和 登入時間。
```sh
who
```
```sh
w
```

## top
查看目前系統服務項目 (類似 windows 工作管理員)，ctrl + c 離開
```sh
top
```

## free 
查看記憶體狀態
```sh
free
```

<br/>

<br/>

# 壓縮檔案指令
## compress
將檔案壓縮成副檔名為 .Z 的檔案
```sh
compress test123                # 壓縮檔案名 test123.Z
```
自訂壓縮檔案名稱
```sh
compress test123 -d xxxx.Z      # 壓縮檔案名 xxxx.Z
```

## gzip
同上，壓縮成副檔名為 .gz 
```sh
gzip test123
```
自訂壓縮檔案名稱
```sh
gzip -d test122 xxxx.gz
```

<br/>

<br/>

# 網路功能
## ifconfig
查詢目前系統網路狀況
```sh
ifconfig
```

## route
查詢網路路由表
```sh
route
```

## netstat
查詢網路狀況
```sh
netstat
```

## hostname
查看主機名稱
```sh
hostname
```

## ping
ping ICMP封包至目標網路 
```sh
ping 8.8.8.8
```

## nslookup
查詢目標網址的 IP
```sh
nslookup www.google.com.tw
```

## traceroute
查詢封包傳送狀態
```sh
traceroute
```

<br/>

<br/>

# 其他指令
## date
查看日期
```sh
date
```

## cal
查看日曆
```sh
cal
```

## grep
查詢某些特定字元，篩選出需要的資訊
```sh
ps -aux|grep sendmail       # 在 ps -aux 指令中，篩選出有關鍵字 sendmail 的資訊
```