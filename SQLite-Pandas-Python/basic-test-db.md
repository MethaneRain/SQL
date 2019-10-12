# Working with SQL via SQLite and Pandas in Python


Make a new database and assign it some tables (columns)
~~~Python

---------------------------------------------------------------------------
import sqlite3

conn = sqlite3.connect('test.db')
print("Opened database successfully")

conn.execute('''CREATE TABLE COMPANY
         (ID INT PRIMARY KEY     NOT NULL,
         NAME           TEXT    NOT NULL,
         AGE            INT     NOT NULL,
         ADDRESS        CHAR(50),
         SALARY         REAL);''')
print("Table created successfully")

#conn.close()

>>> Opened database successfully
>>> Table created successfully
---------------------------------------------------------------------------
~~~


Now some data can be added to the columns in the newly created database (.db file)

~~~Python
---------------------------------------------------------------------------

conn = sqlite3.connect('test.db')
print("Opened database successfully")

conn.execute("INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) \
      VALUES (1, 'Paul', 32, 'California', 20000.00 )");

conn.execute("INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) \
      VALUES (2, 'Allen', 25, 'Texas', 15000.00 )");

conn.execute("INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) \
      VALUES (3, 'Teddy', 23, 'Norway', 20000.00 )");

conn.execute("INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) \
      VALUES (4, 'Mark', 25, 'Richmond ', 65000.00 )");

conn.commit()
print("Records created successfully")
conn.close()

>>> Opened database successfully
>>> Records created successfully
---------------------------------------------------------------------------
~~~

 Now the Pandas library can be introduced with Python to display the selected data


~~~Python
---------------------------------------------------------------------------
import pandas as pd

conn = sqlite3.connect("test.db")
df = pd.read_sql_query("select AGE from COMPANY;", conn)
df

>>>  AGE
>>> 0	32
>>> 1	25
>>> 2	23
>>> 3	25

---------------------------------------------------------------------------
~~~
