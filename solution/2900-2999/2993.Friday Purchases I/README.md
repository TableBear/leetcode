# [2993. Friday Purchases I](https://leetcode.cn/problems/friday-purchases-i)

[English Version](/solution/2900-2999/2993.Friday%20Purchases%20I/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>Table: <code>Purchases</code></p>

<pre>
+---------------+------+
| Column Name   | Type |
+---------------+------+
| user_id       | int  |
| purchase_date | date |
| amount_spend  | int  |
+---------------+------+
(user_id, purchase_date, amount_spend) is the primary key (combination of columns with unique values) for this table.
purchase_date will range from November 1, 2023, to November 30, 2023, inclusive of both dates.
Each row contains user id, purchase date, and amount spend.
</pre>

<p>Write a solution to calculate the <strong>total spending</strong> by users on <strong>each Friday</strong> of <strong>every week</strong> in <strong>November 2023</strong>. Output only weeks that include <strong>at least one</strong> purchase on a <strong>Friday</strong>.</p>

<p>Return <em>the result table ordered by week of month</em><em> in <strong>ascending</strong></em><em><strong> </strong>order.</em></p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Purchases table:
+---------+---------------+--------------+
| user_id | purchase_date | amount_spend |
+---------+---------------+--------------+
| 11      | 2023-11-07    | 1126         |
| 15      | 2023-11-30    | 7473         |
| 17      | 2023-11-14    | 2414         |
| 12      | 2023-11-24    | 9692         |
| 8       | 2023-11-03    | 5117         |
| 1       | 2023-11-16    | 5241         |
| 10      | 2023-11-12    | 8266         |
| 13      | 2023-11-24    | 12000        |
+---------+---------------+--------------+
<strong>Output:</strong> 
+---------------+---------------+--------------+
| week_of_month | purchase_date | total_amount |
+---------------+---------------+--------------+
| 1             | 2023-11-03    | 5117         |
| 4             | 2023-11-24    | 21692        |
+---------------+---------------+--------------+ 
<strong>Explanation:</strong> 
- During the first week of November 2023, transactions amounting to $5,117 occurred on Friday, 2023-11-03.
- For the second week of November 2023, there were no transactions on Friday, 2023-11-10.
- Similarly, during the third week of November 2023, there were no transactions on Friday, 2023-11-17.
- In the fourth week of November 2023, two transactions took place on Friday, 2023-11-24, amounting to $12,000 and $9,692 respectively, summing up to a total of $21,692.
Output table is ordered by week_of_month in ascending order.</pre>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：日期函数**

我们用到的日期函数有：

-   `DATE_FORMAT(date, format)`：将日期格式化为字符串
-   `DAYOFWEEK(date)`：返回日期对应的星期几，1 代表星期日，2 代表星期一，以此类推
-   `DAYOFMONTH(date)`：返回日期对应的月份中的第几天

我们先用 `DATE_FORMAT` 函数将日期格式化为 `YYYYMM` 的形式，然后筛选出 2023 年 11 月且是星期五的记录，然后将记录按照 `purchase_date` 分组，计算出每个星期五的总消费金额。

<!-- tabs:start -->

### **SQL**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```sql
# Write your MySQL query statement below
SELECT
    CEIL(DAYOFMONTH(purchase_date) / 7) AS week_of_month,
    purchase_date,
    SUM(amount_spend) AS total_amount
FROM Purchases
WHERE DATE_FORMAT(purchase_date, '%Y%m') = '202311' AND DAYOFWEEK(purchase_date) = 6
GROUP BY 2
ORDER BY 1;
```

<!-- tabs:end -->