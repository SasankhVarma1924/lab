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
import numpy as np

from sklearn import datasets

from sklearn.model_selection import train_test_split

import matplotlib.pyplot as plt

from matplotlib.colors import ListedColormap

def euclidean_distance(x1, x2):

 return np.sqrt(np.sum((x1 - x2)**2))

class KNN:

 def __init__(self, k=3):
 self.k = k

 def fit(self, X, y):

 self.X_train = X

 self.y_train = y

 def predict(self, X):

 y_pred = [self._predict(x) for x in X]

 return np.array(y_pred)

 def _predict(self, x):

 # Compute distances between x and all examples in the training set

 distances = [euclidean_distance(x, x_train) for x_train in self.X_train]

 # Sort by distance and return indices of the first k neighbors

 k_idx = np.argsort(distances)[:self.k]

 # Extract the labels of the k nearest neighbor training samples

 k_neighbor_labels = [self.y_train[i] for i in k_idx] 

 # return the most common class label

 most_common = Counter(k_neighbor_labels).most_common(1)

 return most_common[0][0]

#Expt3.py file

import numpy as np

from collections import Counter

# import the KNN implementation from knn.py

from knn import KNN 

cmap=ListedColormap(["#000FFF", "#FFF000","#00FF00"])

# Iris data has 50 samples for each different species of Iris flower(total of 150 examples). 

# For each sample we have 4 features sepal length, width and petal length and width and a iris species

name(class/label).

# Load iris dataset

iris=datasets.load_iris()

X,y=iris.data,iris.target

# Viualize sepal length, sepal width data of iris data

print( “Plot showing sepal length, sepal width data of iris data”)

plt.figure()

plt.scatter(X[:,0],X[:,1],c=y,cmap=cmap,edgecolor='none',s=40)

plt.show()

# split data into train and test set

Xtrain, Xtest, Ytrain, Ytest= train_test_split(X,y,test_size=0.2, random_state=1234)

clf=KNN(k=5)

clf.fit(Xtrain,Ytrain)

predictions=clf.predict(Xtest)

acc=np.sum(predictions==Ytest)/len(Ytest)

print("Accuracy of user defined KNN classifier for k=5 neighbors on iris dataset is: %0.3f "%acc)
