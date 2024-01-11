# Instructions:

## Create Tables:

## Create two tables: gift_recipients and gifts.
The gift_recipients table should include columns such as recipient_id, recipient_name, and any other relevant information.
The gifts table should include columns like gift_id, gift_name, and gift_category.
Add Data:

Add at least five rows of sample data to each table. Ensure that there is a common column (e.g., recipient_id or gift_id) that can be used for joining.
## Left Outer Join:

Write a query using Left Outer Join to retrieve a list of all gift recipients and the gifts they are receiving for Christmas. Include recipients who are not receiving any gifts.
Provide a brief explanation of the results obtained from the query.
## Right Outer Join:

Write a query using Right Outer Join to display a list of all gifts and the recipients for each gift. Include gifts that have no assigned recipients.
Explain the results obtained from the query.
## Full Join:

Write a query using Full Join to get a comprehensive list of both gift recipients and gifts. Include recipients without gifts and gifts without assigned recipients.
Discuss the outcomes of the query and when such results might be useful in a Christmas context.


mysql> CREATE DATABASE joins1;
Query OK, 1 row affected (0,02 sec)

mysql> USE joins1;
Database changed
mysql> CREATE TABLE gift_recipients(recipient_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, recipient_name VARCHAR(100));
Query OK, 0 rows affected (0,03 sec)

mysql> INSERT INTO gift_recipients(recipient_name) VALUES ('Bob Robbins'), ('Buffy Bang'), ('Daniel Blue'), ('Valerie Valentine'), ('Victor Frankenstein'), ('Selma Select'), ('Barbara Banana');
Query OK, 7 rows affected (0,03 sec)
Records: 7  Duplicates: 0  Warnings: 0

mysql> INSERT INTO gifts(gift_name, gift_category, recipient_id) VALUES ('Teddy', 'Stuffed Animal', 3), ('Roses', 'Flowers', 2), ('Skat', 'Games', 5), ('Suede: Dog Man Star', 'CDs', 4), ('Gabi', 'Dolls',
7), ('Car', 'Toys', 1);
Query OK, 6 rows affected (0,01 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM gifts;
+---------+---------------------+----------------+--------------+
| gift_id | gift_name           | gift_category  | recipient_id |
+---------+---------------------+----------------+--------------+
|       1 | Teddy               | Stuffed Animal |            3 |
|       2 | Roses               | Flowers        |            2 |
|       3 | Skat                | Games          |            5 |
|       4 | Suede: Dog Man Star | CDs            |            4 |
|       5 | Gabi                | Dolls          |            7 |
|       6 | Car                 | Toys           |            1 |
+---------+---------------------+----------------+--------------+
6 rows in set (0,00 sec)

mysql> SELECT * FROM gift_recipients;
+--------------+---------------------+
| recipient_id | recipient_name      |
+--------------+---------------------+
|            1 | Bob Robbins         |
|            2 | Buffy Bang          |
|            3 | Daniel Blue         |
|            4 | Valerie Valentine   |
|            5 | Victor Frankenstein |
|            6 | Selma Select        |
|            7 | Barbara Banana      |
+--------------+---------------------+
7 rows in set (0,00 sec)

mysql> SELECT r.recipient_id, r.recipient_name, g.gift_name FROM gift_recipients r LEFT JOIN gifts g ON r.recipient_id = g.recipient_id;
+--------------+---------------------+---------------------+
| recipient_id | recipient_name      | gift_name           |
+--------------+---------------------+---------------------+
|            1 | Bob Robbins         | Car                 |
|            2 | Buffy Bang          | Roses               |
|            3 | Daniel Blue         | Teddy               |
|            4 | Valerie Valentine   | Suede: Dog Man Star |
|            5 | Victor Frankenstein | Skat                |
|            6 | Selma Select        | NULL                |
|            7 | Barbara Banana      | Gabi                |
+--------------+---------------------+---------------------+
7 rows in set (0,00 sec)

mysql> SELECT r.recipient_id, r.recipient_name, g.gift_name FROM gift_recipients r RIGHT JOIN gifts g ON r.recipient_id = g.recipient_id;
+--------------+---------------------+---------------------+
| recipient_id | recipient_name      | gift_name           |
+--------------+---------------------+---------------------+
|            3 | Daniel Blue         | Teddy               |
|            2 | Buffy Bang          | Roses               |
|            5 | Victor Frankenstein | Skat                |
|            4 | Valerie Valentine   | Suede: Dog Man Star |
|            7 | Barbara Banana      | Gabi                |
|            1 | Bob Robbins         | Car                 |
+--------------+---------------------+---------------------+
6 rows in set (0,00 sec)

mysql> SELECT r.recipient_id, r.recipient_name, g.gift_name FROM gift_recipients r LEFT JOIN gifts g ON r.recipient_id = g.recipient_id UNION SELECT r.recipient_id, r.recipient_name, g.gift_name FROM gift_recipients r RIGHT JOIN gifts g ON r.recipient_id = g.recipient_id;
+--------------+---------------------+---------------------+
| recipient_id | recipient_name      | gift_name           |
+--------------+---------------------+---------------------+
|            1 | Bob Robbins         | Car                 |
|            2 | Buffy Bang          | Roses               |
|            3 | Daniel Blue         | Teddy               |
|            4 | Valerie Valentine   | Suede: Dog Man Star |
|            5 | Victor Frankenstein | Skat                |
|            6 | Selma Select        | NULL                |
|            7 | Barbara Banana      | Gabi                |
+--------------+---------------------+---------------------+
7 rows in set (0,01 sec)

If I would want to send out the presents, the RIGHT JOIN might be the best option, because I only see the recipients who get a gift. In the LEFT JOIN there is a person that doesn't recieve a gift and I wont see here. In case there are gifts without anyone recieving them, it would be best to use INNER JOIN, but that was not in the exercise. The FULL JOIN I can use to display all the data. 
