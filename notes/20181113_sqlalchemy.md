*Journal*  
Rasmus Groth  
*20181113, Utterslev, Copenhagen, Denmark*

# SQLalchemy
```
$ pip install sqlalchemy
```

### [Creating an engine](https://docs.sqlalchemy.org/en/latest/core/engines.html)
Command:
```py
engine = create_engine(engine_params)
```
Structure of the parameters for the create_engine command
```
dialect+driver://username:password@host:port/database
```
Preparation
```py
from sqlalchemy import create_engine

dialect = "postgresql"
driver = "psycopg2"
host = "localhost",
database = "my_db",
user = os.environ["POSTGRES_UN"],
password = os.environ['POSTGRES_PW']

engine_params = f'{dialect}+{driver}://{user[0]}:{password}@{host[0]}/{database[0]}'

print(engine_params)
```
Console
```
$ postgresql+psycopg2://admin:p@ssw0rd@localhost/my_db
```
### Create the engine
```py
engine = create_engine(engine_params)
```
### Use with pandas
```py
df = pd.read_sql(sql='SELECT * FROM names', con=engine)
print(df)
```
```
    id  name
0   1   Peter
1   2   John
```
