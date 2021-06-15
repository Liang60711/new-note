# 系統管理

## shutdown
會將系統服務關閉後才關機，比<code>poweroff</code>和<code>halt</code>安全。

```sh
# 語法
shutdown [-t seconds] [-rkhncfF] time [message]

# 立馬關機
shutdown now

# 指定時間關機
shutdown 21:30       # 指定幾點幾分
shutdown +10         # 指定 10 分鐘後

# 取消關機 (將指定關機取消)
shutdown -c

# 重新開機
shutdown -r

# 關機後停機
shutdown -h
```

## halt poweroff reboot
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
## useradd

```sh
# 新增使用者
useradd [username]

# 查看使用者
id [username]
```

使用 <code>--shell</code> 選項來指定 shell 類型
```sh
# 新增使用者並指定 shell
useradd -s /bin/tcsh [username]

# 查看使用者 shell 類型
tail -1 /etc/passwd
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
# 顯示日期
date +%F    # 2021-01-01
date +%D    # 01/01/21

# 顯示時間，有空格就加引號
date +%T
date "+%T %D"

# 顯示格式化時間
date "+%Y-%m-%d %H:%M:%S"

## timestamp 秒數
date +%s
```
修改系統時間，要去 timedatectl 將 ntp 關閉才能改
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
hwclock -s

# system to hardware clock 將系統時間複製到硬體時間 (改成系統時間)
hwclock --systohc
hwclock -w
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

翻頁指令:  
* <code>空白鍵</code>: 下一頁
* <code>b</code>: 上一頁
* <code>Ctrl+d</code>: 向上半頁
* <code>Ctrl+u</code>: 向下半頁
* <code>g</code>: 跳至第一行
* <code>G</code>: 跳至最後一行
* <code>數字+g</code>: 跳至第幾行

搜索關鍵字
* 查找不區分大小寫
* <code>/keyword</code>: 從上開始找
* <code>?keyword</code>: 從下開始找
* <code>n</code>: 下一筆資料
* <code>N</code>:上一筆資料

## info 
查詢命令線上文檔
```sh
info [command]
```


## echo 
印出文本
```sh
echo [string]

# 使用跳脫字元選項 <code>-e</code>
echo -e "123\n123"

# 不自動換行
echo -n "123"
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

## 雙引號 單引號
```sh
# 雙引號，弱引用，可以使用變數
echo "$SHELL"       # /bin/bash

# 單引號，強引用
echo '$SHELL'       # $SHELL

# {} 變數正規符號
echo ${SHELL}
```
