~~~Python
conn = sqlite3.connect('test_rpts.db')
print("Opened database successfully")

conn.execute('''CREATE TABLE REPORTS
         (TIME     INT            NOT NULL);''')
print("Table created successfully")
~~~

###

~~~Python
import pandas as pd
df = pd.read_csv('190924_rpts_filtered_torn.csv',parse_dates=True)


~~~

###  With the new database created, the data from the tornado reports ```.csv``` file can be moved over via columns to tables in Pandas ```.to_sql()``` method

~~~Python
con = sqlite3.connect("test_rpts.db")

df.to_sql("storms", con, if_exists='replace', index=False)
~~~

### Grab all the columns from the <i>storms</i> database

~~~Python

df = pd.read_sql_query("SELECT * FROM storms ",con)
df




~~~
