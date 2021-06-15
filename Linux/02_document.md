# 檔案類型
## 概念/規則
1. 嚴格區分大小寫。
2. 目錄也是檔案 (文件)。
3. 同一個路徑下，兩個檔案不能同名。
4. 檔案名不可使用 <code> / </code>；最長不能超過 255 字母；檔案開頭以<code>.</code>開頭為隱藏檔案。
5. dirname 和 basename，以<code> /etc/sysconfig/nwrwork-scripts/ifcfg-eno16777736 </code> 為例。
    * basename: 最右側的檔案或目錄名 <code>ifcfg-eno16777736</code>。
    * dirname: basename 左側的路徑 <code>/etc/sysconfig/nwrwork-scripts </code>。

## 詳細資訊
輸入 <code>ls -l</code> 
```sh
# 取隨便一個檔案為例
drwx------ 2 liang liang 4096 6月 10 15:41 ssh-xxxxxxxxx
```

* 檔案以 10 個字母定義，開頭第 1 個字母為檔案類型 
    * <code>-</code> 普通檔案，即<code>f</code>
    * <code>d</code> 目錄檔案；為路徑映射，非 windows 檔案夾概念。
    * <code>b</code> 塊(隨機)裝置檔案 (block device)；可以隨機存取的設備，如硬碟、光碟機。
    * <code>c</code> 字元(線性)裝置檔案 (character device)；依照先後順序存取資料的設備，如印表機；終端機。
        * major number 主設備號: 標示設備類型。
        * minor number 次設備號: 同一類型中不同的設備。
    * <code>l</code> 符號鏈接檔案 (symbolic link file)；軟鏈接檔案。
    * <code>p</code> 命名管道檔案 (pipe)
    * <code>s</code> 套接字檔案 (socket)

* 後 9 個字母為檔案權限，每 3 位一組 (檔案所有者權限、用戶組權限、其他用戶權限)，每 1 組 rwx 為
    * <code>r</code>: 讀取
    * <code>w</code>: 寫
    * <code>x</code>: 執行

* 數字: 檔案硬鏈接的次數: 2

* 檔案的所有者 (owner): liang

* 檔案的用戶組 (group): liang

* 檔案大小 (size)，單位是字節: 4096

* 時間戳 (timestamp)，最近一次被修改的時間  

    * 訪問 access
    * 修改 modify
    * 改變 change；metadata 元數據

* 檔案名稱

## 編譯方式
* Linux 的 Library 由 glibc 所提供。
1. 動態(鏈接)編譯: 撰寫程式時，不將 lib model 寫進入程式中；執行程式時會調用 lib model；優點是節省記憶體資源。
2. 靜態編譯: 撰寫程式就將 lib model 複製進程式內部中；優點是不管到哪個系統中，都可以執行，不用擔心沒有該 model。

## 檔案種類 (以外部來看)
1. 二進制檔案
2. lib 檔案
3. 配置檔案
4. 幫助檔案


## FHS (Filesystem Hierarchy Standard)
* <code>/bin</code>: 所有用戶可用的基本命令檔案。
* <code>/sbin</code>: 供系統管理使用的工具程式。
* <code>/boot</code>: Linux 核心和開機相關檔案，如 kernel、initramfs(initrd)、grub。
* <code>/dev</code>: 設備(裝置)檔案或特殊檔案。
* <code>/etc</code>: 系統程式的配置檔案。
* <code>/home</code>: 普通用戶家目錄的集中位置；預設路徑 <code>/home/USERNAME</code>。
* <code>/root</code>: root 的家目錄。
* <code>/lib</code>: 為系統啟動或根檔案系統上的應用程式提供共享 lib，以及為 kernel 提供 kernel model。
    * <code>/libc.so.*</code>: 動態鏈接的 C lib。
    * <code>/ld*</code>: 執行時鏈接器。
    * <code>/modules</code>: 用於儲存 kernel model。
* <code>/lib64</code>: 64bit 系統共享 lib。
* <code>/media</code>: 外接式設備，掛載點。
* <code>/mnt</code>: 其他檔案系統的臨時掛載點。
* <code>/opt</code>: 附加應用程式的安裝位置，可選路徑。
* <code>/tmp</code>: 臨時檔案；所有用戶都可以使用。
* <code>/usr</code>: 此目錄包括許多子目錄，用來存放系統指令、安裝程式及套件。
    * <code>/usr/local</code>: 讓系統管理員安裝應用程式、安裝第三方程式(舊版本會安裝在 <code>/opt</code>)。
* <code>/var</code>: 系統執行中，常態性變動的檔案。

<br/>

<br/>


# 指令(命令)
## 指令類型 
* 使用 <code>type COMMAND</code>查看為哪種命令
* 內部命令: 顯示 built-in；shell 自帶的命令。
* 外部命令: 顯示命令路徑。
    * 命令可以有別名，別名可以與原名相同，此時原名被隱藏；如 <code>ls</code> 為 <code>ls --color=auto</code> 的原名。
    * 如果要使用原名使用 <code>\ls</code>
    * 查看/定義別名使用 <code>alias</code>；只對當前 shell 有效。
## basename
查詢 basename
```sh
basename /etc/sysconfig/nwrwork-scripts/ifcfg-eno16777736

# ifcfg-eno16777736
```

## dirname
查詢 dirname 
```sh
dirname /etc/sysconfig/nwrwork-scripts/ifcfg-eno16777736

# /etc/sysconfig/nwrwork-scripts
```

## ls
list
```sh
ls -l           # 顯示詳細資料
ls -a           # 顯示隱藏檔 (以"."開頭的檔案)
ls -A           # 與 -a 相同，少了 . 和 .. 兩個檔案
ls -h           # 做單位轉換
ls -d           # 只顯示目錄
ls -i           # 顯示 inode (index node)
ls -r           # 反向排序檔案
ls -R           # 遞迴列出所有子目錄的檔案
ls -al|more     # 將檔案內容以一頁一頁顯示
ls -ltr         # 檔案依照時間排序，讓最新的檔案排在最後
```

## pwd
printing working directory
```sh
pwd             # 顯示當前路徑
```

## cd
change directory
```sh
cd              # 家目錄
cd ~            # 家目錄 (同上)
cd ~$username   # 切換至指定用戶的家目錄
cd -            # 往返目錄 (遙控器上的返回鍵)
```

## cat
concatenate (連接)，連接檔案並 print 出來，只能印出文字檔案；可以先用 <code>file</code> 查看是否為文字檔案
```sh
# 單個檔案
cat FILENAME

# 可多檔案一同查看
cat FILENAME_1 FILENAME_2

# 增加行號
cat -n FILENAME
```

## tac
與<code>cat</code>相同，只是倒著顯示。
```sh
tac FILENAME
```


## file
查看檔案類型
```sh
file FILENAME
```


## more
一頁一頁查看
```sh
more FILENAME
```

## less
與<code>more</code>類似，多了一個向前翻頁的功能
```sh
# 1
less FILENAME

# 2
man ls|less
```

## head, tail
```sh
# 只看檔案前幾行
head FILENAME

# 只看檔案後幾行
tail FILENAME
```

## alias unalias
查看/定義別名；僅對當前 shell 有效
```sh
# 查看
alias

# 定義
alias NAME="COMMAND"    # alias cls="clear"

# 刪除別名
unalias NAME            # unalias cls
```


## w 類指令
```sh
# 查找命令執行檔路徑
which COMMAND


# 查找與命令同名的所有檔案(使用手冊檔案、二進制檔案)
whereis COMMAND
# -b 僅顯示二進制檔案路徑
# -m 僅顯示使用手冊檔案路徑


# 查找登入用戶
who
# -b 系統啟動時間
# -r 運行級別


# 同 who，多了檢視時間 
w
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