# 用戶、群組、權限管理

## 基礎
* 3A
    * 驗證 (Authentication): 認證用戶為其所宣稱的人的動作。 
    * 授權 (Authorization): 授與已驗證的合作對象權限以執行某些工作的動作 (可以做到什麼程度)。
    * 紀錄 (Accounting): 紀錄此用戶做了甚麼事情；包括量測 (measuring)、監控 (monitoring)、報告 (reporting) 各種資源使用量及事件紀錄（log）。



## 用戶
* 用戶 (user): 每個使用者即是用戶。
* 種類: 
    1. 管理員
    2. 普通用戶: 分為**系統用戶**及**登錄用戶**

* 用戶 ID: 稱為 **UID**；16 bits 二進制 (0-65535)。
    1. 管理員 ID: <code>0</code>
    2. 普通用戶 ID: <code>1-65535</code>
        * 系統用戶 ID: <code>1-999</code>
        * 登錄用戶 ID: <code>1000-60000</code>
    
    * 名稱解析: 轉換 username 和 uid，需要有查詢表，位置在 <code>/etc/passwd</code>。

    * <code>/etc/passwd</code> 用戶查詢表: 
        * 格式為 `name:password:UID:GID:GECOS:directory:shell`

        

<br/>

## 群組
* 群組 (group): 為一個容器，可將有權限相同的用戶歸類至此群組，此群組內的所有用戶彼此權限相同。
* 種類:
    1. 管理員群組
    2. 普通用戶群組: 分為**系統群組**及**登錄群組**

* 群組 ID: 稱為 **GID**；16 bits 二進制 (0-65535)。
    1. 管理群組 ID: <code>0</code>
    2. 普通群組 ID: <code>1-65535</code>
        * 系統群組 ID: <code>1-999</code>
        * 登錄群組 ID: <code>1000-60000</code>
    
    * 名稱解析: 轉換 groupname 和 gid  <code>/etc/group</code>。


## 密碼認證
* 通過事先儲存的密碼，與登錄時提供的密碼進行比對。
* 早期密碼儲存位置同 uid 查詢表中 (<code>/etc/passwd</code>)，後來因安全問題改至
    * 用戶密碼: <code>/etc/shadow</code>。
    * 群駔密碼: <code>/etc/gshadow</code>。

* [加密算法](https://github.com/Liang60711/Note/blob/67087d3e3b2b3f70313359e635eb9e1cfec77e67/Basic/0_osi.md#ssl-%E5%8D%94%E5%AE%9A):
    1. 對稱加密: plain text 加密為 cipher text。
    2. 非對稱加密。

    * 雜湊 (hash) 算法:
        * <code>md5</code>: message digest；128 bits。
        * <code>sha</code> :secure hash algorithm；160 bits。

            ```sh
            # md5sum
            echo 'hash,hash' | md5sum   # 產出 hash 碼

            # sha512sum
            echo 'sha512sum' | sha512sum
            ```
    
    * 如果密碼相同，而產出相同的 hash，同樣有風險，故在進行 hash 算法前，會加入 salt (隨機數)，確保 hash 會不一樣。