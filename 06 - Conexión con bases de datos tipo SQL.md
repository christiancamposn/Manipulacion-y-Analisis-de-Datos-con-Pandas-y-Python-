#Cómo usar Pandas y Python para conectar con tu base de datos SQL
Pandas cuenta con una funcionalidad que facilita el acceso a tus bases de datos tipo SQL, para ello te mostrare algunos ejemplos:

PostgreSQL:
Valida que tengas la librería psycopg2 usando el comando import. Si no está instalada en tu ambiente, usa el comando !pip install psycopg2 en la terminal de python para instalarlo.

Comenzamos cargando las librerías:

import pandas as pd
import psycopg2
Luego creamos el elemento de conexión con el siguieente código:

conn_sql = psycopg2.connect(user = "user_name",
                            password = "password",
                            host = "xxx.xxx.xxx.xxx",
                            port = "5432",
                            database = "postgres_db_name")
Seguido simplemente definimos nuestra query en SQL:

query_sql = '''
select *
from table_name
limit 10
'''
Y creamos nuestro dataframe:

df = pd.read_sql(query_sql, sql_conn)
df.head(5)

#SQL Server:
Valida que tengas la librería pyodbc usando el comando import, si no está instalada en tu ambiente, usa el comando !pip install pyodbc en la terminal python para instalarlo.

Comenzamos cargando las librerías:

import pandas as pd
import pyodbc
Luego creamos el elemento de conexión con el siguiente código:

driver = '{SQL Server}'
server_name = 'server_name'
db_name = 'database_name'
user = 'user'
password = 'password'
sql_conn = pyodbc.connect('''
DRIVER={};SERVER={};DATABASE={};UID={};PWD={};
Trusted_Connection=yes
'''.format(driver, server_name, db_name, user, password))
O si tienes el DSN:

dsn = 'odbc_datasource_name'
sql_conn = pyodbc.connect('''
DSN={};UID={};PWD={};Trusted_Connection=yes;
'''.format(dsn, user, password))
Seguido simplemente definimos nuestra query en SQL:	
query_sql = 'select * from table_name limit 10'

Y creamos nuestro dataframe con:

df = pd.read_sql(query_sql, sql_conn)
df.head(5)

#MySQL / Oracle / Otras:
Valida que tengas la librería sqlalchemy usando el comando import, si no está instalada en tu ambiente, usa el comando !pip install sqlalchemy en la terminal de python para instalarlo.

Comenzamos cargando las librerías:

import pandas as pd
import sqlalchemy as sql
Escogemos nuestra base de datos, Oracle, MySql o la de tu preferencia:
database_type = 'mysql'
database_type = 'oracle'
Luego creamos el elemento de conexión con el siguiente código:

user = 'user_name'
password = 'password'
host = 'xxx.xxx.xxx.xxx:port'
database = 'database_name'

conn_string = '{}://{}:{}@{}/{}'.format(
database_type, user, password, host, database)

sql_conn = sql.create_engine(conn_string)
Seguido simplemente definimos nuestra query en SQL:

query_sql = '''
select *
from table_name
limit 10
'''
Y creamos nuestro dataframe con:

df = pd.read_sql(query_sql, sql_conn)
df.head(5)
La libreria sqlalchemy también soporta PostgreSQL y otras fuentes de datos.
