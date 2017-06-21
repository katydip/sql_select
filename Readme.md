```sql
<!-- 1-Create a list of students showing first and last names only. -->

1-  mysql> select first_name, last_name from student;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| Eric       | Ephram    |
| Greg       | Gould     |
| Adam       | Ant       |
| Howard     | Hess      |
| Charles    | Caldwell  |
| James      | Joyce     |
| Doug       | Dumas     |
| Kevin      | Kraft     |
| Frank      | Fountain  |
| Brian      | Biggs     |
+------------+-----------+
10 rows in set (0.00 sec)

<!-- 2-Create a list of students with all the columns but only if the student has less than 8 years experience -->

2-  mysql> select * from student where years_of_experience < 8;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+------------+-----------+---------------------+------------+
7 rows in set (0.00 sec)

<!-- 3-Create a list of students showing the lastname, startdate, and id columns only and sorted by last_name in ascending sequence -->

3-  mysql> select last_name, start_date, student_id from student order by last_name;
+-----------+------------+------------+
| last_name | start_date | student_id |
+-----------+------------+------------+
| Ant       | 2016-06-02 |          3 |
| Biggs     | 2015-12-25 |         10 |
| Caldwell  | 2016-05-07 |          5 |
| Dumas     | 2016-07-04 |          7 |
| Ephram    | 2016-03-31 |          1 |
| Fountain  | 2016-01-31 |          9 |
| Gould     | 2016-09-30 |          2 |
| Hess      | 2016-02-28 |          4 |
| Joyce     | 2016-08-27 |          6 |
| Kraft     | 2016-04-15 |          8 |
+-----------+------------+------------+
10 rows in set (0.00 sec)

<!-- 4-Create a list of students showing all columns but only if the student first name is Adam, James, or Frank and sort them in last_name descending sequence. -->

4-  mysql> select * from student where first_name IN ('adam', 'james', 'frank') order by last_name desc;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
+------------+------------+-----------+---------------------+------------+
3 rows in set (0.00 sec)

<!-- 5-Create a list of students showing firstname, lastname and startdate where the startdate is between Jan 1, 2016 and June 30, 2016 and order the list by descending start_date sequence. -->
<!-- the dates are strings, require quotes -->

5-  mysql> select first_name, last_name, start_date from student where start_date BETWEEN '2016-01-01' and '2016-06-30' ORDER BY start_date desc;
+------------+-----------+------------+
| first_name | last_name | start_date |
+------------+-----------+------------+
| Adam       | Ant       | 2016-06-02 |
| Charles    | Caldwell  | 2016-05-07 |
| Kevin      | Kraft     | 2016-04-15 |
| Eric       | Ephram    | 2016-03-31 |
| Howard     | Hess      | 2016-02-28 |
| Frank      | Fountain  | 2016-01-31 |
+------------+-----------+------------+
6 rows in set (0.00 sec)


--------------------------------------
<!-- Medium Challenge NOTES
Create the grade table and create a foreign key to it in assignment...

to change the column name we dropped and added the column- the properties in grade_id
must be exact in both tables in order to connect them with foreign keys.

mysql> alter table assignment drop column grade_id;
mysql> ALTER TABLE assignment add column grade_id int;

to create the table grade, we had to have grade_id as an int that we will use as the
foreign key in assignments, and we must have grade to hold characters.

mysql> CREATE TABLE grade (
    ->   `grade_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
    ->   `grade` varchar(30) DEFAULT NULL,
    -> PRIMARY KEY (`grade_id`)
    -> );
Query OK, 0 rows affected (0.02 sec)

How to add a foreign key on command line:

mysql> alter table assignment ADD FOREIGN KEY (grade_id) REFERENCES grade(grade_id);
Query OK, 5 rows affected (0.02 sec)
Records: 5  Duplicates: 0  Warnings: 0 -->


------------------
Medium Challenge
Create the grade table and create a foreign key to it in assignment...

mysql> describe grade;
+----------+------------------+------+-----+---------+----------------+
| Field    | Type             | Null | Key | Default | Extra          |
+----------+------------------+------+-----+---------+----------------+
| grade_id | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| grade    | varchar(30)      | YES  |     | NULL    |                |
+----------+------------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)



mysql> explain assignment;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11) unsigned | NO   | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> select * from assignment;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          2 |              0 |     NULL |        1 |
|             2 |          4 |              0 |     NULL |        2 |
|             3 |          3 |              0 |     NULL |        3 |
|             4 |          7 |              0 |     NULL |        4 |
|             5 |          9 |              0 |     NULL |        5 |
+---------------+------------+----------------+----------+----------+
5 rows in set (0.00 sec)

mysql> explain grade;
+----------+------------------+------+-----+---------+----------------+
| Field    | Type             | Null | Key | Default | Extra          |
+----------+------------------+------+-----+---------+----------------+
| grade_id | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| grade    | varchar(30)      | YES  |     | NULL    |                |
+----------+------------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> select * from grade;
+----------+------------------------------+
| grade_id | grade                        |
+----------+------------------------------+
|        1 | Incomplete                   |
|        2 | Complete and unsatisfactory  |
|        3 | Complete and satisfactory    |
|        4 | Exceeds expectations         |
|        5 | Not graded                   |
+----------+------------------------------+
5 rows in set (0.00 sec)

------------------------------------------
Hard Challenge
Add the constraint to the assignment table that prohibits creating an assignment without an associated student row;  
<!-- notes: aka- make another foreign key in the assignment table so it associates
with student. had to assign student numbers to the rows already created so it would fit with
new rule.  -->

mysql> alter table assignment ADD FOREIGN KEY (student_id) REFERENCES student(student_id);
Query OK, 5 rows affected (0.02 sec)
Records: 5  Duplicates: 0  Warnings: 0
```
