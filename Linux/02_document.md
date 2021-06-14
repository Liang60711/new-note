# 文件類型
## 使用規則
1. 嚴格區分大小寫。
2. 目錄也是文件。
3. 同一個路徑下，兩個文件不能同名。
4. 文件名不可使用 <code> / </code>；最長不能超過 255 字母。
5. dirname 和 basename，以<code> /etc/sysconfig/nwrwork-scripts/ifcfg-eno16777736 </code> 為例。
    * basename: 最右側的文件或目錄名 <code>ifcfg-eno16777736</code>。
    * dirname: basename 左側的路徑 <code>/etc/sysconfig/nwrwork-scripts </code>。


輸入 <code>ls -l</code> 
```sh
# 取隨便一個文件為例
drwx------ 2 liang liang 4096 6月 10 15:41 ssh-xxxxxxxxx
```

* 文件以 10 個字母定義，開頭第 1 個字母為文件類型 
    * <code>-</code> 普通文件
    * <code>d</code> 目錄文件
    * <code>b</code> 塊設備文件 (block)
    * <code>c</code> 字符 設備文件 (character)
    * <code>l</code> 符號鏈接文件 (symbolic link file)
    * <code>p</code> 命令管道文件 (pipe)
    * <code>s</code> 套接字文件 (socket)

* 後 9 個字母為文件權限，每 3 位一組，每 1 組 rwx 為
    * <code>r</code>: 讀取
    * <code>w</code>: 寫
    * <code>x</code>: 執行

* 數字: 文件硬鏈接的次數: 2

* 文件的所有者 (owner): liang

* 文件的屬組 (group): liang

* 文件大小 (size)，單位是字節: 4096

* 時間戳 (timestamp)，最近一次被修改的時間  

    * 訪問 access
    * 修改 modify
    * 改變 change；metadata 元數據

* 文件名稱


<br/>

<br/>


# 指令
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