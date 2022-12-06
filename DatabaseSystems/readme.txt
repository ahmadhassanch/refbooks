
Relation = table
Tuple = row
INTENTION - Structure of table (columns and domain)
EXTENSION - Data in the table (set of tuples in relation)


10:15am

- DDL - Data Definition Language
- DML - Data Manipulation Language 
- DCL - Data Control Language (right and permissions).
   

RELATION - table. R (A1, A2, ..., An), eg: Product (id, name, supplierId, categoryId, price)
ATTRIBUTE - column.  Set A = {id, name, supplierId, categoryId, price}
TUPLE - row, record, (a typical instance of that object)
DOMAIN - Range/allowable values =>  Di = dom(Ai)
DEGREE - number of attributes/columns

CARDINALITY - number of records/tuples

RELATIONAL DATABASE - Collection of tables/relations

INTENTION - Structure of table (columns and domain)
EXTENSION - Data in the table (set of tuples in relation)

10:30-10:45 break

10:45am Lecture 2
Minimality Property : A key is a minimal set of attributes that uniquely identifies a tuple in a relation.
 
Usually there is a set of attributes that uniquely identifies a tuple in a relation.
Such attributes will be collectively referred to as a Superkey

11:05 Lecture 3.
Business/General constraints:
DBMS can enforce some constraints like:
- An employee can not work on more than 2 projects
- An employee must be assigned to at least one project

SQL Identifiers: e.g. Select

Data types:
	BIT, NUMERIC/DECIMAL (XX.XX), FLOAT/REAL/DOUBLE PRECISION (XX.XXXXeXX)
	INTERVAL, CHAR LARGE OBJECT, BINARY LARGE OBJECT (BLOB)
SQL User Defined Type: Used to create a sub-data-type. (Basically restrict domain)
	CREATE DOMAIN domainName AS dataType [DEFAULT defaultValue] [CHECK (condition)]

	CREATE DOMAIN mgrType AS CHAR(5) DEFAULT NULL
	CHECK (
	VALUE IN (
	SELECT eno FROM emp
	WHERE title = 'ME' OR title = 'SA' )
	);

11:40am:

CONSTRAINTS:
	REQUIRED: via NOT NULL 
	DOMAIN:	 via CHAR(2) CHECK (title IN (NULL,'EE','SA','PR','ME'));
		DOMAIN CHECKS can be implemented on entire tuple/row, 
			e.g. degree == 'Y', gap > 3.6. where degree, gap are attributes
	ENTITY INTEGRITY: Primary key should be unique
	REFERENTIAL INEGRITY: Foreign key exists in other table
		e.g. FOREIGN KEY (eno) REFERENCES Emp(eno)
		When update/delete: CASCADE, SET NULL, SET DEFAULT, REJECT(NO ACTION/RESTRICT)
		ON DELETE SET NULL ON UPDATE CASCADE

QUESTION: Why on update cascade??

Primary Key as a Foreign Key in its Own Relation:
     A department table can have parent department
     A person can have a father, ..

ALTER TABLE: ADD (Column), Drop (column), Modify (column), Add Constraint (column)

DROP TABLE

INDEXES: To speed up: e.g. 
	Add index: CREATE INDEX index_name ON table_name (column1); 
	Remove Index: ALTER TABLE table_name DROP INDEX index_name;

DML.
SELECT SUPNR, SUPNAME FROM SUPPLIER WHERE SUPCITY = 'San Francisco' AND SUPSTATUS > 80
SELECT SUPNR, SUPNAME, SUPSTATUS FROM SUPPLIER WHERE SUPSTATUS BETWEEN 70 AND 80
SELECT SUPNR, SUPNAME, SUPSTATUS FROM SUPPLIER WHERE SUPSTATUS IN (70, 75, 80)
SELECT PRODNR, PRODNAME FROM PRODUCT WHERE PRODNAME LIKE '%CHARD%'
SELECT SUPNR, SUPNAME, SUPSTATUS FROM SUPPLIER WHERE SUPSTATUS IS NULL


INSERT INTO PRODUCT (PRODNR, PRODNAME, PRODTYPE, AVAILABLE_QUANTITY) VALUES 
	('980', 'Chateau Angelus, Grand Clu Classé, 1960', 'red', 6), 
	('1000', 'Domaine de la, Bâtard Montrachet', Grand cru, 2010’, 'white', 2)
AGGREGATE FUNCTIONS:
 COUNT, SUM, AVG, VARIANCE, MIN, MAX, and STDEV
	select count(film_id) from film;
	select count(film_id) from film where title like "A%";
	select sum(rental_rate) from film;
	select avg(rental_rate),max(rental_rate),min(rental_rate) from film;

DELETE FROM SUPPLIES WHERE PRODNR IN (SELECT PRODNR FROM PRODUCT WHERE PRODNAME LIKE '%CHARD%')

UPDATE SUPPLIES SET DELIV_PERIOD= DELIV_PERIOD+7 WHERE SUPNR IN
	(SELECT SUPNR FROM SUPPLIER WHERE SUPNAME = 'Deliwines')


3:20pm
Lecture 4: 

Set Operators: Union, Intersection, Difference & Product
Relational Operators: Select, Project, Rename, Join & Division

SET OPERATORS:
--------------
UNION: Union compatible relations:
   They have the same number of attribute types defined on the same domains

  The UNION operator IS applied to two union-compatible relations P and Q

FOR PRODUCT (Cartesian product) we don't need the relations to be compatible.

3:40pm. Zaid went away

In Product, we don't need same attributes, instead attributes are concatenated.
In fact, attributes must not be the same. (My own)







