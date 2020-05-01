---
title: "SQL: Count rows in a table without COUNT()"
date: 2020-05-01T22:33:40+05:30
tags: ["SQL", "Oracle"]
---

# Use a dummy column
- Add a dummy column to all rows with value as 1.
- Print the sum of this dummy column to count the rows.
```sql
SELECT SUM(ROW_COUNT) AS COUNT
FROM (
    SELECT NAME, 1 AS ROW_COUNT
    FROM EMPLOYEE
);
```