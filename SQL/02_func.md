# 函數
## 聚合函數
```SQL
MAX()
MIN()
AVG()
SUM()
COUNT()
COUNT_BIG()		-- 超過 2^23-1 筆資料時使用
```

## 字串函數
```SQL
LEN()			-- 計算字串長度
CONCAT()
CONCAT_WS()		-- CONCAT_WS('-', first_name, last_name); (只有2017以上版本才有)
SUBSTRING()		-- SUBSTRING(username, 1, 10); 取 username 第1到10個字元
```
## 時間函數
```SQL
GETDATE()
GETUTCDATE()
```

format 時間格式
```sql
-- CONVERT(datatype, date, style)
-- style 可查詢 [文件](https://docs.microsoft.com/zh-tw/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-ver15#date-and-time-styles)
SELECT CONVERT(VARCHAR(10), GETDATE(), 111) 	-- 2021/06/03 剛好 VARCHAR(10)
```


## 其他函數
```sql
-- 隨機 0~1 浮點數
RAND() 

-- 隨機整數
FLOOR(RAND()*N)		-- 無條件捨去
CEILING(RAND()*N)	-- 無條件進位
```