# PGCLI Cheat-sheet
[Rasmus Groth](https://github.com/bliiir)
Started: 20181116, Utterslev, Copenhagen, Denmark
Last entry: 20190220, Utterslev, Copenhagen,Denmark

# Short list

| command | Description |
| :-- | :-- |
| ```pgcli -U {system_user_name}``` | Access the [pgcli](https://www.pgcli.com/docs) interface as user {system_user_name} |
| `\l` | list databases |
| `\c {db_name}` | Select database {db_name} |
| `\d` | List all tables in selected database |
| `\d+` | List all tables in selected database with extra info |
| `delete from {table_name};` | Delete all rows from {table_name} |
| `SELECT COUNT(*) FROM {fooTable}` | Get a count of the number of rows in fooTable |

# Comprehensive list

| Command | Description |
|:--| :--|
| `\#` | Refresh auto-completions.|
| `\?` | Show Commands. |
| `\T [format]`| Change the table format used to output results |
| `\c database_name` | Change to a new database.|
| `\conninfo` | Get connection details |
| `\copy [tablename] to/from [filename]` | Copy data between a file and a table.|
| `\d[+] [pattern]`| List or describe tables, views and sequences.|
| `\dD[+] [pattern]` | List or describe domains.|
| `\dT[S+] [pattern]` | List data types|
| `\db[+] [pattern]` | List tablespaces.|
| `\df[+] [pattern]` | List functions.|
| `\di[+] [pattern]` | List indexes.|
| `\dm[+] [pattern]` | List materialized views. |
| `\dn[+] [pattern]` | List schemas.|
| `\ds[+] [pattern]` | List sequences.|
| `\dt[+] [pattern]` | List tables. |
| `\du[+] [pattern]` | List roles.|
| `\dv[+] [pattern]` | List views.|
| `\dx[+] [pattern]` | List extensions. |
| `\e [file]` | Edit the query with external editor. |
| `\h` | Show SQL syntax and help.|
| `\i filename` | Execute commands from file.|
| `\l[+] [pattern]` | List databases.|
| `\n[+] [name] [param1 param2 ...]` | List or execute named queries. |
| `\nd [name]` | Delete a named query.|
| `\ns name query` | Save a named query.|
| `\o [filename]` | Send all query results to file.|
| `\pager [command]` | Set PAGER. Print the query results via PAGER.|
| `\pset [key] [value]` | A limited version of traditional \pset |
| `\q` | Quit pgcli.|
| `\refresh` | Refresh auto-completions.|
| `\sf[+] FUNCNAME` | Show a function's definition.|
| `\timing` | Toggle timing of commands. |
| `\x` | Toggle expanded output.|
| `quit` | Quit pgcli.|

# Links
https://www.pgcli.com/commands
