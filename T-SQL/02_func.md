# 函數
## 數字函數
```sql
MAX()
MIN()
AVG()
SUM()
COUNT()
-- 超過 2^23-1 筆資料時使用
COUNT_BIG()		

-- 隨機 0~1 浮點數
RAND() 

-- 隨機整數
FLOOR(RAND()*N)		-- 無條件捨去
CEILING(RAND()*N)	-- 無條件進位
```

## 字串函數
### 一般
```SQL
LEN()			-- 計算字串長度
UPPER()         -- 轉換成大寫
LOWER()         -- 轉換成小寫
CONCAT()        -- 合併欄位
CONCAT_WS()		-- CONCAT_WS('-', first_name, last_name); (只有2017以上版本才有)
```
### CHARINDEX()
在字串中查找某片段，並返回 INDEX
```SQL
-- CHARINDEX(要查詢的短字串, 要被查詢的長字串 [, 從第幾個 INDEX 開始搜尋])
SELECT CHARINDEX('AA', 'AA3456789');         -- 1 (從1開始)
SELECT CHARINDEX('AA', 'AA3456789AA', 3);    -- 10
```
### PATINDEX()
在字串中查找某片段，並返回 INDEX，但功能比 <code>CHARINDE</code> 多了模糊查找
```SQL
-- PATINDEX ( '%pattern%' , expression )
SELECT PATINDEX('AA', 'AA3456789');          -- 0 (必須完全相同才會返回1)
SELECT PATINDEX('%AA%', 'AA3456789');        -- 1

-- 模糊查找
SELECT PATINDEX('%AA%', 'AA3456789AA');      -- 1
SELECT PATINDEX('AA%', 'AA3456789AA');       -- 1
SELECT PATINDEX('%AA', 'AA3456789AA');       -- 10
```
### STUFF
字串操作，刪除、取代某段
```SQL
-- STUFF( 原字串 , start , length , 要取代的字串 )
SELECT STUFF('AABBCCDD', 5, 2, '');         -- AABBDD
SELECT STUFF('AACCDD', 3, 4, 'BB');         -- AABB
```
### SUBSTRING()
取字串的某段
```SQL
-- SUBSTRING ( 原字串 ,start , length )  
SELECT SUBSTRING(username, 1, 4);           -- user 取 username 第1到4個字元
```
### LEFT()
從左邊開始查找**字元**
```sql
-- LEFT ( character_expression , integer_expression )  
SELECT LEFT('AABBCCDD', 4);         -- AABB
```
### RIGHT()
從右邊開始查找**字元**
```sql
-- RIGHT ( character_expression , integer_expression ) 
SELECT RIGHT('AABBCCDD', 4);        -- CCDD
```
### LTRIM(), RTRIM(), TRIM()
將字串左右、兩邊的空白刪除
```SQL
-- LTRIM ( character_expression ) 
-- RTRIM ( character_expression ) 
-- TRIM ( character_expression )    2017 版本才有

-- 2014 版本只能使用
SELECT LTRIM(RTRIM('   ABC   '));
```

### REPLACE()
將字串指定的部分，進行取代
```SQL
-- REPLACE ( string_expression , string_pattern , string_replacement )
SELECT REPLACE('ABCABC', 'B', 'Z');      -- AZCAZC
```
### REPLICATE
將字串進行複製
```SQL
-- REPLICATE ( string_expression , integer_expression )
SELECT REPLICATE('A', 5);               -- AAAAA
```
### SPACE()
輸出空白字串
```SQL
SELECT CONCAT('A', SPACE(5), 'A');      -- A     A
```
### REVERSE()
將字串反轉
```SQL
-- REVERSE ( string_expression )
SELECT REVERSE('12345')                 -- 54321
```


## 時間函數
### GETDATE()
取得現在時間
```SQL
SELECT GETDATE() 
```
### GETUTCDATE()
取得現在 UTC 時間
```sql
SELECT GETUTCDATE()
```
### CONVERT()
轉換時間格式，
style 可查詢 [文件](https://docs.microsoft.com/zh-tw/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-ver15#date-and-time-styles)
```sql
-- CONVERT ( data_type [(length)] , expression [, style] )
SELECT CONVERT(VARCHAR(10), GETDATE(), 111) 	-- 2021/06/03 剛好 VARCHAR(10)
```




### DATEDIFF()
計算時間差
```sql
-- DATEDIFF(datepart, startdate, enddate)
-- datepart 不用引號
SELECT DATEDIFF(hour, '2019-07-02 19:00:00', GETDATE());
SELECT DATEDIFF(month, '2020-01-01', GETDATE());
```
### DATEADD()
新增間隔，計算新時間
```sql
-- DATEADD(datepart, number, date)
SELECT DATEADD(day, -5, GETDATE());

-- 加上 CONVERT
SELECT CONVERT(VARCHAR(20), DATEADD(month, 3, GETDATE()), 120)
```
### DATEPART()
取日期的某一個單位
datepart 寫法參考[文件](https://docs.microsoft.com/zh-tw/sql/t-sql/functions/datepart-transact-sql?view=sql-server-ver15#arguments)
```sql
-- DATEPART(datepart, date)
-- 返回 INT
SELECT DATEPART(DD, '2020-01-01');      -- 返回 1 (INT)
SELECT DATEPART(YYYY, '2021-01-01');    -- 返回 2021
```
### DATENAME()
取日期的某一個單位，同上
```SQL
-- DATENAME()
-- 返回 VARCHAR
SELECT DATENAME(DD, '2020-01-01');      -- 返回 1 (VARCHAR)
```
### YEAR(), MONTH(), DAY()
```SQL
-- 返回 INT
SELECT YEAR(GETDATE())      -- 2021
SELECT MONTH(GETDATE())     -- 6
SELECT DAY(GETDATE())       -- 4
```

## 其他函數
### CAST
轉換資料型態
```SQL
-- CAST ( expression AS data_type [ ( length ) ] )
-- INT >> VARCHAR
SELECT 'AA' + CAST(123 AS VARCHAR(5));          -- AA123

-- FLOAT >> INT
SELECT CAST(12.5 AS INT);                       -- 12

-- VARCHAR >> DATETIME
SELECT CAST('2021-01-01' AS  DATETIME);         -- 2021-01-01 00:00:00.000
```

## CASE()
條件判斷
```SQL
-- 簡單運算
SELECT 
    CASE username 
        WHEN 'John' THEN 'Y'
        ELSE 'N'
    END
FROM user;

-- 使用條件
SELECT 
    CASE
        WHEN score in ('A+', 'A', 'A-') THEN '優'
        WHEN score in ('B+') THEN '普' 
        ELSE '差'
    END
FROM score;
```