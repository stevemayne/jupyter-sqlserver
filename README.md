# jupyter-sqlserver
Jupyter notebook with ODBC support and MS SQL Server driver

```bash
docker run  -p 8888:8888 -v ~/notebooks/:/home/jovyan/work stevemayne/jupyter-sqlserver
```

## Example notebook content

```python
import pandas as pd
import pyodbc
import numpy as np
import matplotlib as plt
import getpass
%matplotlib inline
%load_ext sql

server = "x.x.x.x"
db = "my_db"
username = "my_username"
password = getpass.getpass("Database password? ")

#Either connect using pyodbc:
conn = pyodbc.connect("Driver={sqlsrv};Server={%s};Database={%s};uid={%s};pwd={%s}" % (server, db, username, password))
sql = "Select * from TABLE"
data = pd.read_sql(sql, conn)

#Or use ipython-sql extension:
connection_string = "mssql+pyodbc://{username}:{password}@{server}/{db}?driver=sqlsrv".format(username=username, password=password, db=db, server=server)
%sql $connection_string
result = %sql SELECT * FROM TABLE
data = result.DataFrame()

```
