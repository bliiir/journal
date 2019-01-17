# PGCLI Cheat-sheet
[Rasmus Groth](https://github.com/bliiir)  
Started: 20181116, Utterslev, Copenhagen, Denmark  
Last entry: 20190107, Utterslev, Copenhagen,Denmark



| command | effect |
| :-- | :-- |
| ```pgcli -U {system_user_name}``` | Access the [pgcli](https://www.pgcli.com/docs) interface as user {system_user_name} |
| ```\l``` | list databases |
| ```\c {db_name}``` | Select database {db_name} |
| ```\d``` | List all tables in selected database |
| ```\d+``` | List all tables in selected database with extra info |
| ```delete from {table_name};``` | Delete all rows from {table_name} |
| ```SELECT COUNT(*) FROM {fooTable}``` | Get a count of the number of rows in fooTable |
