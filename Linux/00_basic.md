# 參考 Reference
[鳥哥的linux私房菜](https://linux.vbird.org/)

<br/>

<br/>

# 名詞解釋
### kernel
將硬體的計算能力提供給上層的軟體使用，提供方式為 system call。


### library
kernel 的 system call 過於底層，所以造成系統開發難度高，故將一個或多個 system call 的功能封裝成較高級的 library API，不能單獨執行，只能被調用。


### .dll
Windows 的動態連結函式庫 (Dynamic link library)，在 windows 中的

### .so 文件
Linux 的動態連結函式庫 (Shared object)

### FHS
檔案系統階層標準 (Filesystem Hierarchy Standard)，定義 Linux 作業系統中的主要目錄及目錄內容。


<br/>

<br/>

# 基本原則
1. 複雜的任務，都是由小程序組合而成。
2. 一切皆文件。
3. 盡量避免捕獲用戶接口 (避免和用戶交互)。
4. 配置文件為文本格式。
5. CLI:  
    * 命令提示符 (prompt) 分為
        * #: root
        * $: 普通用戶
    
    * 命令格式: 為 **命令 command**，**選項 options**，**參數 arguments**

        ```sh
        # ls為命令 -l為選項 /ect為參數
        ls -l /ect
        ```
6. Shell 種類:
    * GUI:
        1. Gnome
        2. KDE
        3. XFace
    * CLI:
        1. bash (功能最齊全)
        2. csh
        3. zsh
        4. ksh
        5. tcsh

7. 切換虛擬terminal <code>Ctrl</code> + <code>Alt</code> + <code>F1~F6</code>

8. 切換用戶 switch user

    ```sh
    # 切換
    su -l 用戶名
    ```
    ```sh
    # 退出
    exit
    ```


<br>

<br/>

# 文件類型
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

# 命令類型
### 查詢命令類型
輸入 <code>type</code> 指令來查看命令類型。
1. 內建命令: shell builtin，是 shell 的一部分，通常在運行 Linux 時，就會被載入在記憶體中。
2. 外部命令: 因為使用上太佔記憶體，在系統載入時，不一定會一起被載入到記憶體中，需要時再調用；**在文件系統的某個路徑下，會有一個與命令相同的執行文件**。

### 查詢環境變數
輸入 <code>printenv</code>，會找到 PATH。
```sh
# 路徑使用 : 隔開 代表尋找文件的優先順序
PATH=/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```

### hash 暫存
輸入 <code>hash</code>，查詢命令暫存表。

系统下會有 hash 表，每個 shell 獨立，每當執行命令時，hash 表會記錄命令的路徑。第一次執行命令 shell 會從 PATH 路徑下找該命令的路徑，當第二次使用該命令時，shell 會查看 hash 表，沒有該命令才會去 PATH 路徑下尋找。

hash 表作用: 提高命令的調用速度 (cache is king)。
