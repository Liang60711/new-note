# 名詞解釋
## OLTP
* Online Transactional Processing，規則為一個事務 (Transaction) 完成後才會執行下一筆，確保整個系統的資料**一致性**，須符合 ACID 規範。
    * `ACID`: 指資料庫管理系統（DBMS）在寫入或更新資料的過程中，為保證事務（transaction）是正確可靠的，必須具備的四個特性：
        1. 原子性（atomicity，或稱不可分割性）
        2. 一致性（consistency）
        3. 隔離性（isolation，又稱獨立性）
        4. 持久性（durability）

<br/>

* 使用: 銀行系統就是一個非常標準使用 OLTP 的系統，銀行系統必須要確保您每次拿取的資料都是一致性而且是完全正確的。

<br/>

## OLAP
* Online Analytical Processing，OLAP 的系統可以讓數據聚合 (data aggregation) 以及批次處理 (Batch processing)，OLAP 大部分是用來做歷史資料的分析以及報告。OLAP 可以很快的使用 Query 去得到數據洞察得到數據聚合後的結果。

## OLTP 和 OLAP 比較
* OLTP 重視數據處理以及一致性
* OLAP 重視數據分析。
* 通常他們兩個會搭配使用，儲存資料的時候先存到 OLTP 中確保數據一致性，要做分析的時候再使用 OLAP 做重要報表。

<br/>

## Row-oriented 和 Column-oriented Database
* Row-oriented: 適合用在網站、APP，可以很快速的讀取一個用戶 (id) 的完整訊息；如 MySQL、MSSQL。

* Column-oriented: 適合在數據分析的時候去使用，在某些欄位的掃描 max, min 時他不會像是 Row-based 要把整個 database 全部掃描完才能夠運算，可以一次讀取欄位訊息；如 Clickhouse、Redshift。

## 正規化 和 反正規化
* 正規化: 在設計 MySQL 資料庫的時候，會有 Primary Key, Foreign Key 把相同的數據拉開到不同的 Table 中，對儲存效率比較好(不會有重複項)。

* 反正規化: 先將不同的 Table Join 至一張表中儲存，效能理論上比較好。