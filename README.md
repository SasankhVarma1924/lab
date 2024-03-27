import mysql.connector 

#SET MYSQL CONNECTION 

mydb = mysql.connector.connect( 

 host="localhost", 

 user="root", 

 password="Root123$" 

) 

#CREATE CURSOR INSTANCE 

mycursor = mydb.cursor() 

print("Database connection successful ",mydb) 

#CREATE DATABASE mydatabase 

mycursor.execute("CREATE DATABASE IF NOT EXISTS mydatabase") 

#SHOW DATABASE

mycursor.execute("SHOW DATABASES") 

for x in mycursor: 

 print(x) 

#SET mydatabase connection 

mydb = mysql.connector.connect(
host="localhost", 

 user="root", 

 password="Root123$", 

 database="mydatabase" 

) 

#CREATE CURSOR INSTANCE 

mycursor = mydb.cursor() 

print("Database connection successful ",mydb) 

#Change to mydatabase and CREATE TABLE customers with id, name and address fields 

mycursor.execute("use mydatabase") 

mycursor.execute("CREATE TABLE IF NOT EXISTS customers (id INT AUTO_INCREMENT

PRIMARY KEY, name VARCHAR(255), address VARCHAR(255))") 

print("Created customers table") 

#SHOW TABLES in mydatabase 

mycursor.execute("SHOW TABLES") 

for x in mycursor: 

 print(x) 

#INSERT MULTIPLE RECORDS into customer table 

sql = "INSERT INTO customers (name, address) VALUES (%s, %s)" 

val = [ 

 ('Peter', 'Lowstreet 4'), 

 ('Amy', 'Apple st 652'), 

 ('Hannah', 'Mountain 21'), 

 ('Michael', 'Valley 345'), 

 ('Sandy', 'Ocean blvd 2'), 

 ('Vicky', 'Yellow Garden 2'),

 ('Ben', 'Park Lane 38'), 

 ('William', 'Central st 954'), 

 ('Chuck', 'Main Road 989'), 

 ('Viola', 'Sideway 1633') 

] 

mycursor.executemany(sql, val) 

mydb.commit() 

print(mycursor.rowcount, "records were inserted.") 

#RETRIEVE DATA from customers table 

mycursor.execute("SELECT * FROM customers ") 

myresult = mycursor.fetchall() 

for x in myresult: 

 print(x) 

#WHERE CLAUSE and LIKE WILDCARDS 

sql = "SELECT * FROM customers WHERE address LIKE '%way%'" 

mycursor.execute(sql) 

myresult = mycursor.fetchall() 

for x in myresult:
print(x) 

#UPDATING RECORDS 

my_sql = "UPDATE customers SET address = 'Road N0 4, Gandhinagar' WHERE name= ‘Ben’ 

my_cursor.execute(my_sql) 

mydb.commit() 

#ORDERING RESULTS 

my_cursor.execute("SELECT * FROM customers ORDER BY name DESC") 

result = my_cursor.fetchall() 

for row in result: 

 print(row) 

#DELETE RECORDS 

my_sql = "DELETE FROM customers WHERE name = 'Hannah'" 

my_cursor.execute(my_sql) 

mydb.commit() 

#DROP TABLE customers

sql = "DROP TABLE customers" 

mycursor.execute(sql) 

mydb.commit() 

OUTPUT:

Database connection successful <mysql.connector.connection_cext.CMySQLConnection object at

0x0000028AEDC3CAF0>

('information_schema',)

('mydatabase',)

('mysql',)

('performance_schema',)

('sakila',)

('sys',)

('world',)

Database connection successful <mysql.connector.connection_cext.CMySQLConnection object at

0x0000028AEDC46640>

Created customers table

('customers',)

10 records were inserted.

(1, 'Peter', 'Lowstreet 4')

(2, 'Amy', 'Apple st 652')

(3, 'Hannah', 'Mountain 21')

(4, 'Michael', 'Valley 345')

(5, 'Sandy', 'Ocean blvd 2')

(6, 'Vicky', 'Yellow Garden 2')

(7, 'Ben', 'Park Lane 38')

(8, 'William', 'Central st 954')

(9, 'Chuck', 'Main Road 989')

(10, 'Viola', 'Sideway 1633')

(10, 'Viola', 'Sideway 1633')

Displaying records in descending order
(8, 'William', 'Central st 954')

(10, 'Viola', 'Sideway 1633')

(6, 'Vicky', 'Yellow Garden 2')

(5, 'Sandy', 'Ocean blvd 2')

(1, 'Peter', 'Lowstreet 4')

(4, 'Michael', 'Valley 345')

(3, 'Hannah', 'Mountain 21')

(9, 'Chuck', 'Main Road 989')

(7, 'Ben', 'Road N0 4, Gandhinagar')

(2, 'Amy', 'Apple st 652')
