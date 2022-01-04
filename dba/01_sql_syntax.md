# ORDER BY + CASE WHEN
`ORDER BY` 加上條件進行篩選
1. 將 [stock為0的欄位] 排序設為 0， [stock大於1000的欄位] 排序為 1，依照數字大小排序，所以 [stock為0的欄位] 會置頂，[stock大於1000的欄位] 成為第二置頂，其他為第三順位。
2. 可以使用 `ASC` `DESC` 排序，但不能使用小括號。

```sql
SELECT id, title, stock, displayorder FROM goods
ORDER BY
    CASE
        WHEN stock=0 THEN 0
        WHEN stock>1000 THEN 1
    END ASC,
    displayorder DESC;
```

將 title 為 apple 的欄位設為置頂
```sql
SELECT id, title, stock, displayorder FROM goods
ORDER BY 
    CASE
        WHEN title="apple" THEN 0 ELSE 1
    END;
```