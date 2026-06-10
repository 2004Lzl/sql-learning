# SQL 时间日期函数速查表

## 一、提取函数

```sql
-- TIME() - 提取时间部分
TIME('2026-06-08 14:25:30')  -- 返回 '14:25:30'
TIME('14:25:30')              -- 返回 '14:25:30'

-- DATE() - 提取日期部分
DATE('2026-06-08 14:25:30')  -- 返回 '2026-06-08'
DATE('2026-06-08')            -- 返回 '2026-06-08'

-- YEAR() / MONTH() / DAY()
YEAR('2026-06-08')   -- 返回 2026
MONTH('2026-06-08')  -- 返回 6
DAY('2026-06-08')    -- 返回 8

-- HOUR() / MINUTE() / SECOND()
HOUR('14:25:30')     -- 返回 14
MINUTE('14:25:30')   -- 返回 25
SECOND('14:25:30')   -- 返回 30

-- DAYOFWEEK() / WEEKDAY()
DAYOFWEEK('2026-06-08')  -- 返回 2（周日=1，周一=2...）
WEEKDAY('2026-06-08')    -- 返回 0（周一=0，周二=1...）

--DATE_FORMAT()
DATE_FORMAT('2026-06-08','%Y-%M') -- 返回 2026-06
DATE_FORMAT('2026-06-08','%Y-%M-01') -- 返回 2026-06-01
```
## 二、计算函数

```sql
-- TIMESTAMPDIFF() - 计算时间差（指定单位）
-- 语法：TIMESTAMPDIFF(单位, 开始时间, 结束时间)
TIMESTAMPDIFF(SECOND, '2026-06-08 14:00:00', '2026-06-08 14:01:30')  -- 返回 90
TIMESTAMPDIFF(MINUTE, '2026-06-08 14:00:00', '2026-06-08 15:30:00')  -- 返回 90
TIMESTAMPDIFF(HOUR, '2026-06-08 08:00:00', '2026-06-08 17:00:00')     -- 返回 9
TIMESTAMPDIFF(DAY, '2026-06-01', '2026-06-08')                         -- 返回 7
TIMESTAMPDIFF(MONTH, '2026-01-01', '2026-06-08')                       -- 返回 5
TIMESTAMPDIFF(YEAR, '2020-01-01', '2026-06-08')                        -- 返回 6
-- 支持单位：MICROSECOND, SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER, YEAR

-- TIMEDIFF() - 返回时间差（TIME类型）
TIMEDIFF('14:30:00', '14:00:00')  -- 返回 '00:30:00'
-- 限制：不能超过 838 小时

-- DATEDIFF() - 返回日期差（天数）
DATEDIFF('2026-06-08', '2026-06-01')  -- 返回 7
-- 注意：DATEDIFF(结束, 开始)，与 TIMESTAMPDIFF 参数顺序相反

-- 时间加减函数
DATE_ADD('2026-06-08', INTERVAL 10 DAY)    -- 返回 '2026-06-18'
DATE_SUB('2026-06-08', INTERVAL 1 MONTH)   -- 返回 '2026-05-08'

-- 直接加减（特定数据库）
'2026-06-08' + INTERVAL 7 DAY              -- MySQL
NOW() + INTERVAL 7 DAY                      -- PostgreSQL
```
