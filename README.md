# jupyter-sqlserver
Jupyter notebook with ODBC support and MS SQL Server driver

```bash
docker run -p 8888:8888 stevemayne/jupyter-sqlserver
```

## Example notebook content

```python
import pandas as pd
import pyodbc
import numpy as np
import matplotlib as plt
import getpass
%matplotlib inline

server = "x.x.x.x"
db = "my_db"
username = "my_username"
password = getpass.getpass("Database password?")

conn = pyodbc.connect("Driver={sqlsrv};Server=%s;Database=%s;uid=%s;pwd=%s" % (server, db, username, password))

sql = "Select * from TABLE"
data = pd.read_sql(sql, conn)
```
