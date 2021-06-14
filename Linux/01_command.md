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
## poweroff reboot
關機 重啟
```sh
# 關機
poweroff
# 重啟
reboot
```

## tty
查看目前終端設備
```sh
tty
```

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

# 時間指令

## 硬體時間 系統時間
* 硬體時間: 指主機板上的時鐘裝置。  
* 系統時間: 指 kernel 的時鐘。當 Linux 啟動時，系統時間會去讀取硬體時間的設定，之後系統時間即獨立運作。

## date
查看系統時間
```sh
# date [option] [+format]
# 有空格就加引號
date +%T
date '+%T %D'

# 顯示格式化時間
date "+%Y-%m-%d %H:%M:%S"
```
修改系統時間，不改要去 timedatectl 將 ntp 關閉
```sh
## CC 為幾世紀
date [MMDDhhmm[[CC]YY][.ss]]
```

查看硬體時間
```sh
hwclock
```
修改硬體時間
```sh
hwclock --set --date "2021-01-01 00:00:00"
```
同步時間
```sh
# hardware clock to system 將硬體時間複製到系統時間 (改成硬體時間)
# 需先關閉 timedatectl 的 ntp
hwclock --hctosys

# system to hardware clock 將系統時間改成硬體時間 (改成系統時間)
hwclock --systohc
```


## cal
查看當月日曆
```sh
cal
```
查看整年年曆
```
cal 2021
```

## timedatectl
查看系統時間資訊
```sh
timedatectl
```
設定時區
```sh
timedatectl set-timezone "Asia/Taipei"
```
設定時區 (使用 GUI)
```sh
dpkg-reconfigure tzdata
```

設定系統時間
```sh
timedatectl set-time "2021-01-01"
```
如果系統有設定以 ntp 自動校時，在手動更改日期與時間時，就出現這樣的錯誤訊息： <code>Failed to set time: Automatic time synchronization is enabled</code>

所以要先將 ntp 關閉
```sh
# 關閉
timedatectl set-ntp no

# 打開
timedatectl set-ntp yes
```

<br/>

<br/>

# 其他指令

## grep
查詢某些特定字元，篩選出需要的資訊
```sh
ps -aux|grep sendmail       # 在 ps -aux 指令中，篩選出有關鍵字 sendmail 的資訊
```

## man 
查看該指令的操作手冊，分章節:
1. 用戶命令 (/bin, /usr/bin, /usr/local/bin)
2. 系統調用
3. lib 用戶
4. 特殊文件 (設備文件)
5. 文件格式 (配置文件的語法)
6. 遊戲
7. 雜項 (miscellaneous)
8. 管理命令 (/sbin, /usr/sbin, /usr/local/sbin)
9. kernel routines

```sh
# man <章節> <指令>
man 4 tty
```
一次列出所有章節
```sh
# man -aw <指令>
man -aw passwd
```


每個章節的大綱，又分為:
* NAME: 名稱
* SYNOPSIS: 語法
* DESCRIPTION: 詳盡說明各選項功能
* OPTIONS: 說明選項意義
* FILES: 相關配置文件
* BUGS:
* EXAMPLES: 範例
* SEE ALSO: 另外參照

## echo 
印出文本
```sh
echo [string]
```
使用跳脫字元選項 <code>-e</code>
```sh
echo -e "123\n123"
```

## printf
與 ehco 相比，不會自動換行
```sh
$ echo "Hello, Shell"
# Hello, Shell

$ printf "Hello, Shell\n"
# Hello, Shell
```

## echo $SHELL
查看當前 shell 類型
```sh
echo $SHELL
```