### Working with MS SQL Server

#### MS SQL Server  `Port 1433`

* To connect to the server
```
sqsh -S server -U username -P password
-S server
-U username
-P password
```

* Execute a Query
```
SELECT * FROM reindeer.dbo.names;
```
The ` ;` indicates the end of the SQL query, while `go` sends a SQL batch to the database.

* Some MS SQL Servers have `xp_cmdshell`
* The command syntax is `xp_cmdshell 'COMMAND';`
eg.  `xp_cmdshell 'whoami';`

Any command we pass to `xp_cmdshell` will run as nt `service\mssqlserver`
