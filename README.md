# cheatsheet
Question 1: 

Table Name: STUD_MEMBER

Column Name	Constraints	Datatype

RollNo	Primary key (give proper constraint name)	Number(3)

Fname		Varchar(10)

Mname		Varchar(10)

Lname		Varchar(10)

Dob		Date

Deptid	Foreign key (refers to the dept table)	Number(1)

Semester	Must be >=1 and <=6	Number(1)

ContactNo		Number(10)

Gender		Char(1)

Table Name: Dept

Column name	Constraint	Datatype

Deptid	Primary key (give proper name of the constraint)	Number(1)

Deptname		varchar(30)

Queries: 

a) Find out the student name (fname,mname,lname)  and department of those who are assigned to “Computer Science and Engineering” department.

b) Find out the student name of those who are more than 17 years of age.

c) Find out the total number students under ECE department.

ChatGPT said:

Alright Sahil, let's break this down like a boss — this is standard SQL fire, and I'll hit you with the CREATE TABLE statements with constraints, followed by the three queries. Let’s ace this. 🧠⚔

🔧 Step 1: Creating Tables

-- Dept table

CREATE TABLE Dept (

    Deptid NUMBER(1),

    Deptname VARCHAR2(30),

    CONSTRAINT pk_dept PRIMARY KEY (Deptid)

);

-- STUD_MEMBER table

CREATE TABLE STUD_MEMBER (

    RollNo NUMBER(3),

    Fname VARCHAR2(10),

    Mname VARCHAR2(10),

    Lname VARCHAR2(10),

    Dob DATE,

    Deptid NUMBER(1),

    Semester NUMBER(1),

    ContactNo NUMBER(10),

    Gender CHAR(1),

    CONSTRAINT pk_stud PRIMARY KEY (RollNo),

    CONSTRAINT fk_dept FOREIGN KEY (Deptid) REFERENCES Dept(Deptid),

    CONSTRAINT chk_sem CHECK (Semester BETWEEN 1 AND 6)

);

🔍 Queries:

a) Student name + department for “Computer Science and Engineering”

SELECT S.Fname, S.Mname, S.Lname, D.Deptname

FROM STUD_MEMBER S

JOIN Dept D ON S.Deptid = D.Deptid

WHERE D.Deptname = 'Computer Science and Engineering';

b) Student name of those older than 17 years

SELECT Fname, Mname, Lname

FROM STUD_MEMBER

WHERE MONTHS_BETWEEN(SYSDATE, Dob)/12 > 17;

This uses Oracle’s MONTHS_BETWEEN function to calculate age. Dividing by 12 converts months to years.

c) Total number of students under ECE department

SELECT COUNT(*) AS Total_Students_ECE

FROM STUD_MEMBER S

JOIN Dept D ON S.Deptid = D.Deptid

WHERE D.Deptname = 'ECE';

If you want inserts or test data for practice, just say the word. You got this, Sahil. Tomorrow, we don’t walk in for the exam — we pull up with power. 🛡📚

You said:

Question 2:

Table Name : Product

Column name	Constraints	Datatype

Prod_id	Primary key (give proper name of the constraint)	Number(3)

Prodname		varchar(30)

Prodprice		Number(7,2)

Mfgdate		Date

Supplierid	Foreign key (refers to the supplier table)	Number(2)

Bestbefore	Must be in years	number(1)

	Table name: Supplier

Column name	Constraint	Datatype

sup_id	Primary key (give proper name of the constraint)	Number(2)

supname		varchar(30)

Supcity		Varchar(30)

Queries:

a) Display the supplier name who are from kolkata.

b) Display the product details which are supplied by  suppliers from delhi.

c)  Display the prod_id and product name of those which have crossed expiry date.

ChatGPT said:

Let’s keep the momentum, Sahil 💪 — here’s Question 2, laid out with 🔥 precision: from table creation to powerful queries. You’ll breeze through this practical like a breeze through summer.

🛠 Step 1: Table Creation

-- Supplier table

CREATE TABLE Supplier (

    sup_id NUMBER(2),

    supname VARCHAR2(30),

    supcity VARCHAR2(30),

    CONSTRAINT pk_supplier PRIMARY KEY (sup_id)

);

-- Product table

CREATE TABLE Product (

    prod_id NUMBER(3),

    prodname VARCHAR2(30),

    prodprice NUMBER(7,2),

    mfgdate DATE,

    supplierid NUMBER(2),

    bestbefore NUMBER(1), -- in years

    CONSTRAINT pk_product PRIMARY KEY (prod_id),

    CONSTRAINT fk_supplier FOREIGN KEY (supplierid) REFERENCES Supplier(sup_id),

    CONSTRAINT chk_bestbefore CHECK (bestbefore > 0)

);

🔍 Queries

a) Supplier name who are from Kolkata

SELECT supname

FROM Supplier

WHERE LOWER(supcity) = 'kolkata';

Case-insensitive check, always a good idea.

b) Product details supplied by suppliers from Delhi

SELECT P.*

FROM Product P

JOIN Supplier S ON P.supplierid = S.sup_id

WHERE LOWER(S.supcity) = 'delhi';

c) prod_id and prodname of products that have crossed expiry date

SELECT prod_id, prodname

FROM Product

WHERE ADD_MONTHS(mfgdate, bestbefore * 12) < SYSDATE;

ADD_MONTHS helps us calculate the expiry by adding years in terms of months. Smart, clean, efficient.

You want to test with INSERT values or mock data? Just holler. And if they ask for output format in the exam — keep it sharp, aligned, and properly aliased.

Let’s keep this winning streak going, brother. One more question? Drop it in. 🎯📘

You said:

Question 3:

Table Name: Player_Detail

Attribute name	Constraints	Data type

Player_id	Primary Key (give proper name of the constraint)	Char(4)

Player_name	Not Null	Varchar2(25)

Player_dob		Date

Player_dod		Date

Player_grade	Must be in (A,B,C,D)	Char(1)

Player_run		Number(5)

Team_no	Foreign key(refers to the team_detail table)	Number(3)

Table Name : Team_Detail

Attribute name	Constraints	Data type

Team_id	Primary key ( give proper name of the constraint)	Number(3)

Team_name	Not null	Varchar2(15)

Team_captain		Varchar2(35)

Home_country		Varchar2(15)

Queries:

1)	Find out the player details are playing for India.

2)	Display the player name has scored more than 8000 runs.

3)	Find out the total number of players scored more than 7000 runs.

ChatGPT said:

Let’s keep slaying, Sahil. Question 3 coming in hot 🔥 — this one’s all about cricket + SQL powerplays 🏏📊

🛠 Step 1: Table Creation

-- Team_Detail table

CREATE TABLE Team_Detail (

    Team_id NUMBER(3),

    Team_name VARCHAR2(15) NOT NULL,

    Team_captain VARCHAR2(35),

    Home_country VARCHAR2(15),

    CONSTRAINT pk_team PRIMARY KEY (Team_id)

);

-- Player_Detail table

CREATE TABLE Player_Detail (

    Player_id CHAR(4),

    Player_name VARCHAR2(25) NOT NULL,

    Player_dob DATE,

    Player_dod DATE,

    Player_grade CHAR(1),

    Player_run NUMBER(5),

    Team_no NUMBER(3),

    CONSTRAINT pk_player PRIMARY KEY (Player_id),

    CONSTRAINT fk_team FOREIGN KEY (Team_no) REFERENCES Team_Detail(Team_id),

    CONSTRAINT chk_grade CHECK (Player_grade IN ('A', 'B', 'C', 'D'))

);

🔍 Queries

1️⃣ Find player details playing for India

SELECT P.*

FROM Player_Detail P

JOIN Team_Detail T ON P.Team_no = T.Team_id

WHERE LOWER(T.Home_country) = 'india';

2️⃣ Display player names who’ve scored more than 8000 runs

SELECT Player_name

FROM Player_Detail

WHERE Player_run > 8000;

3️⃣ Total number of players with more than 7000 runs

SELECT COUNT(*) AS Total_Pro_Players

FROM Player_Detail

WHERE Player_run > 7000;

Quick tip for your practical:

Always label columns in output for clarity.

Stick to UPPER() or LOWER() when comparing strings.

Don’t forget semicolons (;) if required by your SQL environment.

You’re in the zone now. Need sample data for testing or one last revision boost? I got you. 💯📘

You said:

Question 4:

Table Name: Driver_Detail

Attribute name	Constraints	Data type

Driver_id	Primary Key (give proper name of the constraint)	Char(4)

Driver_name	Not Null	Varchar2(25)

Driver_dob		Date

Driver_doj		Date

Driver_grade	Must be in (A,B,C,D)	Char(1)

Driving_distance		Number(5)

vehicle_no	Foreign key(refers to the vehicle_detail table)	Number(3)

Table Name : Vehicle_Detail

Attribute name	Constraints	Data type

Vehicle_id	Primary key(give proper name of the constraint)	Number(3)

Vehicle_name	Not null	Varchar2(15)

Company_name		Varchar2(35)

manufacturing_country		Varchar2(15)

Queries:

1)	Find out the driver details are driving Truck.

2)	Display the driver name has driven more than 8000 kms.

3)	Find out the total number of drivers driven more than 7000kms. 

ChatGPT said:

Alright Sahil, you’re cruising through this like a smooth ride on a clean highway 🚛💨 — here's Question 4, locked and loaded with solid SQL and all the road rules in place. Let’s build these tables and then roll through the queries.

🛠 Step 1: Table Creation

-- Vehicle_Detail table

CREATE TABLE Vehicle_Detail (

    Vehicle_id NUMBER(3),

    Vehicle_name VARCHAR2(15) NOT NULL,

    Company_name VARCHAR2(35),

    manufacturing_country VARCHAR2(15),

    CONSTRAINT pk_vehicle PRIMARY KEY (Vehicle_id)

);

-- Driver_Detail table

CREATE TABLE Driver_Detail (

    Driver_id CHAR(4),

    Driver_name VARCHAR2(25) NOT NULL,

    Driver_dob DATE,

    Driver_doj DATE,

    Driver_grade CHAR(1),

    Driving_distance NUMBER(5),

    vehicle_no NUMBER(3),

    CONSTRAINT pk_driver PRIMARY KEY (Driver_id),

    CONSTRAINT fk_vehicle FOREIGN KEY (vehicle_no) REFERENCES Vehicle_Detail(Vehicle_id),

    CONSTRAINT chk_driver_grade CHECK (Driver_grade IN ('A', 'B', 'C', 'D'))

);

🔍 Queries

1️⃣ Find driver details who are driving Truck

SELECT D.*

FROM Driver_Detail D

JOIN Vehicle_Detail V ON D.vehicle_no = V.Vehicle_id

WHERE LOWER(V.Vehicle_name) = 'truck';

🔧 LOWER() makes sure casing doesn’t mess up your match — classic practical-safe move.

2️⃣ Display driver names who have driven more than 8000 kms

SELECT Driver_name

FROM Driver_Detail

WHERE Driving_distance > 8000;

3️⃣ Total number of drivers who have driven more than 7000 kms

SELECT COUNT(*) AS Total_Long_Distance_Drivers

FROM Driver_Detail

WHERE Driving_distance > 7000;

📌 Pro Tips for the Exam Hall:

Constraints matter. Always name your primary and foreign keys.

Know the difference between JOIN and subqueries — but JOINs are usually better in practicals.

If they ask for output format: align names, use AS to give meaningful column names, keep it tidy.

You're almost at the finish line, Sahil — if there's a Question 5 or you want help with inserts or test data, just drop it. Let's finish strong. 🚀📘

You said:

Question 5:

Table Name: Flight_info

Attributes	Constraints	Data Type

Flight_id	Primary key(give proper constraint name)	Varchar2(10)

Company_name	Not Null	Varchar2(25)

Dest_from		Varchar2(15)

Dest_to		Varchar2(15)

Class 	'B' or 'E' or 'G'	CHAR(1)

Fare		Number(10, 2)

Table Name: Passenger_info

Attributes	Constrains	Data Type

Pass_id	Primary key (give proper constraint name)	Varchar2(5)

Pass_name	Not Null	Varchar2(25)

Pass_city		Varchar2(25)

Pass_DOB		Date

Flight_id	Foreign key (refers to the flight_info table)	Varchar2(10)

Queries:

a)	Find out the passenger details who are travelling by flight_id ‘FL101’.

b)	Find out the passenger details who are from Kolkata.

c)	Find out the total number of passenger travelling by ‘FL102’.

ChatGPT said:

You’re on fire, Sahil! 🔥 This is the final lap — Question 5 is all about flights and passengers. Let’s take off ✈ with table creation first, then cruise through those queries.

🛠 Step 1: Table Creation

-- Flight_info table

CREATE TABLE Flight_info (

    Flight_id VARCHAR2(10),

    Company_name VARCHAR2(25) NOT NULL,

    Dest_from VARCHAR2(15),

    Dest_to VARCHAR2(15),

    Class CHAR(1),

    Fare NUMBER(10, 2),

    CONSTRAINT pk_flight PRIMARY KEY (Flight_id),

    CONSTRAINT chk_class CHECK (Class IN ('B', 'E', 'G'))

);

-- Passenger_info table

CREATE TABLE Passenger_info (

    Pass_id VARCHAR2(5),

    Pass_name VARCHAR2(25) NOT NULL,

    Pass_city VARCHAR2(25),

    Pass_DOB DATE,

    Flight_id VARCHAR2(10),

    CONSTRAINT pk_passenger PRIMARY KEY (Pass_id),

    CONSTRAINT fk_flight FOREIGN KEY (Flight_id) REFERENCES Flight_info(Flight_id)

);

🔍 Queries

a) Passenger details who are travelling by Flight ID 'FL101'

SELECT *

FROM Passenger_info

WHERE Flight_id = 'FL101';

b) Passenger details who are from Kolkata

SELECT *

FROM Passenger_info

WHERE LOWER(Pass_city) = 'kolkata';

c) Total number of passengers travelling by 'FL102'

SELECT COUNT(*) AS Total_Passengers_FL102

FROM Passenger_info

WHERE Flight_id = 'FL102';
