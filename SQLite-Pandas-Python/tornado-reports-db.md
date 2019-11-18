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

```

Time	F_Scale	Location	County	State	Lat	Lon	Comments
0	2230	UNK	12 N SIERRA BLANCA	HUDSPETH	TX	31.35	-105.36	TWO LANDSPOUT TORNADOES WERE OBSERVED NORTH OF...
1	2231	UNK	5 SE CUSHING	IDA	IA	42.42	-95.60	BRIEF ROPE TORNADO. STILL EXTREME ROTATION TO ...
2	2242	UNK	5 NNE IDA GROVE	IDA	IA	42.41	-95.44	(FSD)
3	2257	UNK	5 SE PISGAH	HARRISON	IA	41.79	-95.85	TWO BRIEF TOUCHDOWNS. (OAX)
4	2306	UNK	6 SW DUNLAP	HARRISON	IA	41.79	-95.68	TWO BRIEF TOUCHDOWNS OF A TORNADO IN A FIELD. ...
5	23	UNK	6 SW ISABEL	BARBER	KS	37.41	-98.64	BRIEF ROPE TORNADO LASTING LESS THAN MINUTE RE...
6	48	UNK	1 ENE ELK MOUND	DUNN	WI	44.88	-91.67	*** 2 INJ *** A TORNADO SPUN UP JUST EAST OF E...
7	50	UNK	2 ENE ELK MOUND	DUNN	WI	44.88	-91.66	CONFIRMED TORNADO ON THE GROUND EAST OF ELK MO...
8	58	UNK	LAKE CITY	WABASHA	MN	44.45	-92.27	EF0 TORNADO CONFIRMED IN LAKE CITY. DAMAGE TO ...
9	226	UNK	4 SSW GREENWOOD	CLARK	WI	44.72	-90.63	TORNADO TRACKED FROM SOUTH SOUTHWEST OF GREENW...
```


~~~
