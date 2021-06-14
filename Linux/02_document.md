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
