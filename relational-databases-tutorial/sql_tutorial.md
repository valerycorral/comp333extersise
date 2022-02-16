# SQL Tutorial

An introduction to SQL based on <https://www.w3schools.com/sql/sql_primarykey.asp>
for COMP 333 Software Engineering
Created by Sophie Cohen (scohen02@wesleyan.edu)

## 1. Grocery List Table

Set up this table:

```sql
CREATE TABLE groceries (id INTEGER PRIMARY KEY, name TEXT, quantity INTEGER, aisle INTEGER);
INSERT INTO groceries VALUES (1, "Bananas", 4, 7);
INSERT INTO groceries VALUES(2, "Peanut Butter", 1, 2);
INSERT INTO groceries VALUES(3, "Dark Chocolate Bars", 2, 2);
INSERT INTO groceries VALUES(4, "Ice cream", 1, 12);
INSERT INTO groceries VALUES(5, "Cherries", 6, 2);
INSERT INTO groceries VALUES(6, "Chocolate syrup", 1, 4);
```

### Grocery List Queries

Some questions for the students to practice using SELECT, SUM, MAX

#### (a) Select the entire table

```sql
SELECT * FROM groceries;
```

#### (b) Select names of items

```sql
SELECT name FROM groceries;
```

#### (c) Sort by aisle number

```sql
SELECT * FROM groceries ORDER BY aisle;
```

#### (d) Print the products in aisles bigger than 5, and sort

```sql
SELECT * FROM groceries WHERE aisle > 5 ORDER BY aisle;
```

#### (e) Find the sum of the quantities

```sql
SELECT SUM(quantity) FROM groceries;
```

#### (f) Find the maximum quantity

```sql
SELECT MAX(quantity) AS `Maximum Quantity` FROM groceries;
```

## 2. Exercise Table

Set up this table:

```sql
CREATE TABLE exercise_logs
    (id INTEGER PRIMARY KEY AUTO_INCREMENT,
    type TEXT,
    minutes INTEGER,
    calories INTEGER,
    heart_rate INTEGER);

INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 30, 100, 110);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("biking", 10, 30, 105);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 200, 120);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("dancing", 15, 165, 120);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("tree climbing", 25, 72, 80);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("rowing", 30, 70, 90);
INSERT INTO exercise_logs(type, minutes, calories, heart_rate) VALUES ("hiking", 60, 80, 85);
```

### Exercise Queries

Practice with other statements: OR, AND, ORDER BY, GROUP

#### (a) Print exercises with calories more than 80, sorted

```sql
SELECT * FROM exercise_logs WHERE calories > 80 ORDER BY calories;
```

#### (b) Print exercises with calories more than 80 and longer than 20 minutes

```sql
SELECT * FROM exercise_logs WHERE calories > 50 AND minutes < 30;
```

#### (c) Print exercises with calories more than 80 or heart rate more than 100

```sql
SELECT * FROM exercise_logs WHERE calories > 50 OR heart_rate > 100;
```

#### (d) Print biking, hiking, and rowing using IN

```sql
SELECT * FROM exercise_logs WHERE type IN ("biking", "hiking", "rowing");
```

#### (e) Find the total and average calories for each type of exercise

```sql
SELECT type, SUM(calories) AS total_calories FROM exercise_logs GROUP BY type;
SELECT type, AVG(calories) AS total_calories FROM exercise_logs GROUP BY type;
```

#### (f) Print the exercises with total calories greater than 150

```sql
SELECT type, SUM(calories) AS total_calories FROM exercise_logs
    GROUP BY type
    HAVING total_calories > 150;
```

#### (g) Print the exercises that appear two or more times

```sql
SELECT type FROM exercise_logs GROUP BY type HAVING COUNT(*) >= 2;
```

#### (h) If the max heart rate is 190, create a column called hr_zone as follows: "above max", "above target" is 90% of max, "within target" is 50% of max, "below target" is anything else. Print exercise, heart rate, and hr zone

```sql
SELECT type, heart_rate,
    CASE
        WHEN heart_rate > 190 THEN "above max"
        WHEN heart_rate > ROUND(0.90 * 190) THEN "above target"
        WHEN heart_rate > ROUND(0.50 * 190) THEN "within target"
        ELSE "below target"
    END as "hr_zone"
FROM exercise_logs;
```

## 3. Students Tables

Set up two tables:

```sql
CREATE TABLE students (id INTEGER PRIMARY KEY AUTO_INCREMENT,
    first_name TEXT,
    last_name TEXT,
    email TEXT,
    phone TEXT,
    birthdate TEXT);

INSERT INTO students (first_name, last_name, email, phone, birthdate)
    VALUES ("Peter", "Rabbit", "peter@rabbit.com", "555-6666", "2002-06-24");
INSERT INTO students (first_name, last_name, email, phone, birthdate)
    VALUES ("Alice", "Wonderland", "alice@wonderland.com", "555-4444", "2002-07-04");
```

```sql
CREATE TABLE student_grades (id INTEGER PRIMARY KEY AUTO_INCREMENT,
    student_id INTEGER,
    test TEXT,
    grade INTEGER);

INSERT INTO student_grades (student_id, test, grade)
    VALUES (1, "Nutrition", 95);
INSERT INTO student_grades (student_id, test, grade)
    VALUES (2, "Nutrition", 92);
INSERT INTO student_grades (student_id, test, grade)
    VALUES (1, "Chemistry", 85);
INSERT INTO student_grades (student_id, test, grade)
    VALUES (2, "Chemistry", 95);
```

### Students Queries

Different ways to join the tables

#### (a) Cross join the tables

```sql
SELECT * FROM student_grades, students;
```

#### (b) Implicit inner join

```sql
SELECT * FROM student_grades, students
    WHERE student_grades.student_id = students.id;
```

#### (c) Explicit inner join using JOIN

```sql
SELECT students.first_name, students.last_name, students.email, student_grades.test, student_grades.grade FROM students
    JOIN student_grades
    ON students.id = student_grades.student_id
    WHERE grade > 90;
```

#### (d) Introduce another table

```sql
CREATE TABLE student_projects (id INTEGER PRIMARY KEY AUTO_INCREMENT,
    student_id INTEGER,
    title TEXT);

INSERT INTO student_projects (student_id, title)
    VALUES (1, "Carrotapault");
```

Explain how this allows you to combine tables of different sizes

#### (e) Use a left outer join to print out the student first name, last name, and project

```sql
SELECT students.first_name, students.last_name, student_projects.title
    FROM students
    LEFT OUTER JOIN student_projects
    ON students.id = student_projects.student_id;
```

## 4. SQL Working in Conjunction with PHP in a Web App

This is where the real power of PHP comes in. Check the code samples on the
class website.
