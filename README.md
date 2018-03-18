UPDATE t1 SET t1.Field = t2.Field
FROM Table1 as t1
INNER JOIN Table2 as t2 on t1.Key = t2.Key
WHERE t2.FilterField = 'abc'

UPDATE t1 SET t1.Field = t2.Field
FROM (SELECT DISTINCT Table1 as t1
INNER JOIN Table2 as t2 on t1.Key = t2.Key
WHERE t2.FilterField = 'abc') t3
WHERE t1.key = t3.key
