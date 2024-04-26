Pet Taxi is a service, similar to Uber, that provides local travel services to pets that need to go to the groomer, vet, park, etc.  Pet Taxi can simply drop off the pet or they can stay with the pet during the visit and then return them home.  Pet Taxi charges $25 per hour for this service.  Currently, they only provide services for dogs, cats, birds, and fish.  

Pet Taxi needs a database to track the information about their company.   

Create and ERD with appropriate entities, attributes, keys, relationships, and data types.  

Keep in mind that Many-to-Many relationships should not be implemented in the database.  These relationships should be broken into One-to-Many relationships using Associative Entities. 

[ My PetTaxi Database ]
![image](https://github.com/ConnorLBrown/PetTaxi-Database/assets/122556149/b88ae799-e8f2-4ffb-917c-35baff943ade)





Based on your Pet Taxi database design:

1.) Create your database including all tables and appropriate constraints.

2.) Enter at least three records in each table. You must include yourself in the data.

3.) Demonstrate the use queries, including joins of at least three tables, to extract data from the database. Think of what kinds of questions would be relevant to the employees, customers, etc.

What to turn in:

4.) Execute a DESCRIBE command on each of your tables and copy and past the result into the assignment or into a document you upload.

5.) Do the same for 2-3 join queries that you developed in #3. Submit the query and the results


RESULTS:

mysql> describe owner;
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| cid  | int         | NO   | PRI | NULL    | auto_increment |
| fname     | varchar(50) | YES  |     | NULL    |                |
| lname     | varchar(50) | YES  |     | NULL    |                |
| DOB       | date        | YES  |     | NULL    |                |
| phone_num | varchar(15) | YES  |     | NULL    |                |
| address   | varchar(50) | YES  |     | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
6 rows in set (0.03 sec)

mysql> describe drivers;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| did | int         | NO   | PRI | NULL    | auto_increment |
| fname    | varchar(50) | YES  |     | NULL    |                |
| lname    | varchar(50) | YES  |     | NULL    |                |
| cartype  | varchar(50) | YES  |     | NULL    |                |
| DOB      | date        | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> describe pettaxi;
+----------+------+------+-----+---------+-------+
| Field    | Type | Null | Key | Default | Extra |
+----------+------+------+-----+---------+-------+
| did | int  | NO   | PRI | NULL    |       |
| aid | int  | NO   | PRI | NULL    |       |
+----------+------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> describe appointment;
+-----------------+-------------+------+-----+---------+----------------+
| Field           | Type        | Null | Key | Default | Extra          |
+-----------------+-------------+------+-----+---------+----------------+
| appid         | int         | NO   | PRI | NULL    | auto_increment |
| cid       | int         | YES  | MUL | NULL    |                |
| did        | int         | YES  | MUL | NULL    |                |
| sid       | int         | YES  | MUL | NULL    |                |
| appdate        | date        | YES  |     | NULL    |                |
| location | varchar(30) | YES  |     | NULL    |                |
| lengthmins      | int         | YES  |     | NULL    |                |
+-----------------+-------------+------+-----+---------+----------------+
7 rows in set (0.01 sec)

mysql> describe transaction;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| sid | int          | NO   | PRI | NULL    | auto_increment |
| type      | varchar(50)  | YES  |     | NULL    |                |
| price     | decimal(3,2) | YES  |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

mysql> describe taxi;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| tid  | int         | NO   | PRI | NULL    | auto_increment |
| model    | varchar(50) | YES  |     | NULL    |                |
| year     | varchar(4)  | YES  |     | NULL    |                |
| did | int         | YES  | MUL | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)

mysql> describe animal;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| aid     | int         | NO   | PRI | NULL    | auto_increment |
| breed | varchar(50) | YES  |     | NULL    |                |
| name  | varchar(50) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+

 

 

 

mysql> select drivers.fname, drivers.lname, appointment.appdate, appointment.location from drivers inner join appointment on appointment.appid=drivers.did;
+--------+--------+------------+--------------------+
| fname  | lname  | appdate   |   location    |
+--------+--------+------------+--------------------+
| Donald  | Trump | 2023-03-15 |  1202 Florence Boulevard    |
| Joe  | Biden  | 2023-03-10 | 332 MaryLee Drive |
| Derek | Jeter   | 2023-03-05 | 336 Oak Street    |
+--------+--------+------------+--------------------+ 

mysql> select owner.fname, owner.lname, appointment.appdate, appointment.location from owner inner join appointment on appointment.appid=owner.cid;
+---------+---------+------------+--------------------+
| fname   | lname   | appdate   |  location    |
+---------+---------+------------+--------------------+
| Connor    | Brown   | 2023-03-19 | 753 Nellie Avenue   |
| Danny | McBride  | 2023-03-20 | 553 OakView Circle |
| George   | Clooney| 2023-03-21 | 905 Rodeo Drive    |
+---------+---------+------------+--------------------+

mysql> select owner.fname, owner.lname, animal.breed from owner inner join animal on animal.aid =owner.cid;
+---------+---------+---------------------+
| fname   | lname   |   breed        |
+---------+---------+---------------------+
| Connor    | Brown   | German Shepard   |
| Danny |  McBride |  Bull mastiff     |
| George    | Clooney | Pomeranian |
+---------+---------+---------------------+
