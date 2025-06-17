Difference between data and information
![[Pasted image 20250610134749.png]]
![[Pasted image 20250610134905.png]]
A **database** is a collection of related data that is stored and organized in a structured manner to enable information to be stored, retrieved, manipulated, and managed efficiently.
The data in a database can be queried, updated, and manipulated using specialized software called a **database management system** (DBMS), which provides tools and interfaces for creating, modifying, and querying the data.

#### The Most Common Constraints

- NOT NULL ensures a column cannot have a NULL value.
- DEFAULT specifies a default value for a column in a table when a new record is inserted, if no value is provided for that column. When a column is defined with a DEFAULT constraint, it means that if no value is specified for that column during an INSERT operation, the default value will be inserted instead.
- UNIQUE ensures that a column or set of columns in a table contains only unique values. When a column or set of columns is defined with the UNIQUE constraint, it means that the combination of values in that column or set of columns must be unique across all records in the table. It is important to note that the UNIQUE constraint does NOT prevent NULL values from being inserted into a column or set of columns. If NULL values are allowed in a column or set of columns, they are treated as unique values, which means that a NULL value can be present in the column or set of columns without violating the UNIQUE constraint.
- KEY ensures the uniqueness and integrity of data in a table.
- CHECK ensures that all the values in a column satisfy certain conditions.
![[Pasted image 20250610150638.png]]
![[Pasted image 20250610150807.png]]
![[Pasted image 20250610150933.png]]
![[Pasted image 20250610153907.png]]
![[Pasted image 20250610154441.png]]
![[Pasted image 20250610154633.png]]
Normalization
![[Pasted image 20250610155759.png]]

A table is in **2nd Normal Form** (2NF) if it satisfies the criteria of 1NF and further complies with one additional rule:

- Each table cell should contain an atomic value.
- All the columns in a table should have unique names.
- Each row in a table must be unique (no rows may be duplicated).
- Values stored in a column should be of the same data type and the same domain.
- The order in which data is stored does not matter.
- A table must have a unique primary key that is used to identify each record differently.
- **Each non-key attribute must be fully functional, dependent on the primary key**

A table is in **3rd Normal Form** (3NF) if it satisfies the criteria of 2NF and further complies with one additional rule:

- Each table cell should contain an atomic value.
- All the columns in a table should have unique names.
- Each row in a table must be unique (no rows may be duplicated).
- Values stored in a column should be of the same data type and the same domain.
- The order in which data is stored does not matter.
- A table must have a unique primary key that is used to identify each record differently.
- Each non-key attribute must be fully functional, dependent on the primary key
- **No non-key attribute may be transitively dependent on a key candidate**

## Entity-Relationship Modelling
### One-to-one relationships between two entities
![[Pasted image 20250611142857.png]]
### One-to-many relationships between two entities
![[Pasted image 20250611142912.png]]
### Many-to-many relationships between two entities
![[Pasted image 20250611142929.png]]
It is difficult to implement many to many relationship in database system, usually it is decomposed to several one to many relationships
![[Pasted image 20250611143030.png]]
### Recursive relationships
It is possible for an entity to have a relationship with itself; for example, an entity Staff could have a relationship with itself, as one member of staff could supervise other staff. This is known as a recursive or involute relationship, and would be represented in an entity-relationship diagram as shown below.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_20.png)
### Mandatory and optional relationships
1. **Mandatory for both entities:** A member of staff must be assigned to a given department, and any department must have staff. There can be no unassigned staff, and it is not possible to have an 'empty' department.
    
2. **Mandatory for one entity, optional for the other:** Any member of staff must be attached to a department, but it is possible for a department to have no staff allocated.
    
3. **Optional for one entity, mandatory for the other:** A member of staff does not have to be placed in a department, but all departments must have at least one member of staff.
    
4. **Optional for both entities:** A member of staff might be assigned to work in a department, but this is not compulsory. A department might, or might not, have staff allocated to work within it.

### One-to-one relationships and participation conditions
#### Both ends mandatory
It might be the case that each performer has only one agent, and that all bookings for any one performer must be made by one agent, and that agent may only make bookings for that one performer. The relationship is one-to-one, and both entities must participate in the relationship.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_21.png)

The solid circle at each end of the relationship shows that the relationship is mandatory in both directions; each performer must have an agent, and each agent must deal with one performer.
#### One end mandatory, other end optional:
It might be possible for agents to make bookings that do not involve performers; for example, a venue might be booked for an art exhibition. Each performer, however, must have an agent, although an agent does not have to make a booking on behalf of a performer.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_22.png)

The solid circle at the performer end of the relationship illustrates that a performer must be associated with an agent. The hollow circle at the agent end of the relationship shows that an agent could be associated with a performer, but that this is not compulsory. Each performer must have an agent, but not all agents represent performers.

 ### One-to-many relationships and participation conditions

It might be the case that a performer has only one agent, and that all bookings for any one performer must be made by one agent, although any agent may make bookings for more than one performer.

#### Both ends mandatory:

A performer must have one or more bookings; each booking must involve one performer.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_24.png)

The membership class is mandatory for both entities, as shown by the solid circle. In this case, it is not possible for a booking to be made for an event that does not involve a performer (for example, a booking could not be for an exhibition).

#### One end mandatory, other end optional:

A performer must have one or more bookings, but a booking might not involve a performer (e.g. a booking might be for an exhibition, not a performer).

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_25.png)

The solid circle shows the compulsory nature of the relationship for a performer; all performers must have bookings. The hollow circle shows that it is optional for a booking to involve a performer. This means that a performer must have a booking, but that a booking need not have a performer.

#### One end optional, other end mandatory:

A performer might have one or more bookings; each booking must involve one performer.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_26.png)

The membership class is mandatory for a booking, but optional for a performer. This means that it would not be possible for a booking to be for an exhibition, as all bookings must involve a performer. On the other hand, it is not compulsory for a performer to have a booking.

#### Both ends optional:

A performer might have one or more bookings; a booking might be associated with a performer.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_27.png)

In this case, a booking could be for an exhibition as it is optional for a booking to involve a performer, as indicated by the hollow circle. A performer might decline to accept any bookings; this is acceptable, as it is optional for a performer to have a booking (shown by the hollow circle).

### Many-to-many relationships and participation conditions

We could say that there is a many-to-many relationship between performers and agents, with each agent making bookings for many performers, and each performer having bookings made by many agents. We know that we need to decompose many-to-many relationships into (usually) two one-to-many relationships, but we can still consider what these many-to-many relationships would look like before this decomposition has taken place. We will see later that many-to-many relationships can be converted into relations either after they have been decomposed, or directly from the many-to-many relationship. The result of the conversion into relations will be the same in either case.

#### Both ends mandatory:

An example here might be where each performer must be represented by one or more agents, and each agent is required to make bookings for a number of performers.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_28.png)

There is a many-to-many relationship between the two entities, in which both entities must participate. Agents are not allowed to make bookings for events that do not involve performers (such as conferences or exhibitions). Performers must have bookings made by agents, and are not allowed to make their own bookings.

#### One end mandatory, other end optional:

In this example, it is still necessary for performers to be represented by a number of agents, but the agents now have more flexibility as they do not have to make bookings for performers.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_29.png)

There is a many-to-many relationship between the two entities; one must participate, but it is optional for the other entity.

#### One end optional, other end mandatory:

Here, performers have the flexibility to make their own bookings, or to have bookings made by one or more agents. Agents are required to make bookings for performers, and may not make arrangements for any other kind of event.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_30.png)

There is a many-to-many relationship between the two entities; it is optional for one to participate, but participation is mandatory for the other entity.

#### Both ends optional

Here, performers and agents are both allowed a degree of flexibility. Performers may make their own bookings, or may have agents make bookings for them. Agents are permitted to make bookings for a number of performers, and also have the ability to make other kinds of bookings where performers are not required.

![](https://www.cs.uct.ac.za/mit_notes/database/htmls/media/chp06_31.png)

There is a many-to-many relationship between the two entities; participation is optional for both entities.

These many-to-many relationships are likely to be decomposed into one-to-many relationships. The mandatory/optional nature of the relationship must be preserved when this happens.
## Weak and strong entities

An entity set that does not have a primary key is referred to as a weak entity set. The existence of a weak entity set depends on the existence of a strong entity set, called the identifying entity set. Its existence, therefore, is dependent on the identifying entity set.

The relationship must be many-to-one from weak to identifying entity. Participation of the weak entity set in the relationship must be mandatory. The discriminator (or partial key) of a weak entity set distinguishes weak entities that depend on the same specific strong entity. The primary key of a weak entity is the primary key of the identifying entity set + the partial key of the weak entity set.

**Example: Many payments are made on a loan**

- Payments donвЂ™t exist without a loan.
    
- Multiple loans will each have a first, second payment and so on. So, each payment is only unique in the context of the loan which it is paying off.
    

The weak entity is commonly represented by two boxes.

![[Pasted image 20250611144511.png]]

The payment is a weak entity; its existence is dependent on the loan entity.

## SQL commands
![[Pasted image 20250611162703.png]]
![[Pasted image 20250611164800.png]]
![[Pasted image 20250611165358.png]]
Combining two columns into one. 
SELECT SUBSTRING ('Leorando', 1, 3); - Leo
SELECT POSITION ('L', in 'Leorando'); - 1
![[Pasted image 20250611170121.png]]
PG_TYPEOF converts to certain data type, in this case to integer
COALESCE return first not null value
![[Pasted image 20250611171736.png]]
![[Pasted image 20250611171905.png]]
![[Pasted image 20250611171916.png]]
![[Pasted image 20250611171928.png]]
![[Pasted image 20250611171941.png]]
![[Pasted image 20250611172005.png]]
![[Pasted image 20250611172018.png]]
![[Pasted image 20250611172034.png]]
![[Pasted image 20250611173412.png]]
Subquery serves as data source, that can be further filtered
![[Pasted image 20250611173249.png]]
The query display the actors who played at three longest film 
![[Pasted image 20250611173635.png]]
In this case subquery is used to filter the data from main query
![[Pasted image 20250611174948.png]]
The code displays the movie title and release year of BURT TEMPLE. note this query may take long time to execute.
![[Pasted image 20250611180113.png]]
The code above functionally same, but faster
It's important to note that when dealing with NULL values, IN and NOT IN behave differently than EXISTS and NOT EXISTS. IN and NOT IN treat NULL values as unknown, while EXISTS and NOT EXISTS treat NULL values as nonexistent. Therefore, when dealing with NULL values, it's generally safer to use EXISTS and NOT EXISTS.
![[Pasted image 20250611180903.png]]
The code is also functionally same, but more readable. Avoid the nesting 
![[Pasted image 20250612140549.png]]
![[Pasted image 20250612140650.png]]
advantage: more readable, from top to button 
![[Pasted image 20250612140832.png]]
![[Pasted image 20250612140953.png]]
Set operations: Union all combines all rows, Union removes duplicates, Intersect only those who present in both table, EXCEPT remains only those who are present at first table and upsent at second one
## The SQL CASE Expression
![[Pasted image 20250612145115.png]]
EXAMPLE:
SELECT name, CASE WHEN monthlymaintenance> 100 THEN 'expensive'
ELSE 'cheap' END as cost
FROM cd.facilities


EXAMPLE 
SELECT cdm.firstname || ' ' ||cdm.surname as member, cdf.name as facility,
CASE 
	WHEN cdb.memid = 0 THEN cdf.guestcost * cdb.slots
	ELSE cdf.membercost * cdb.slots
	END AS cost
FROM cd.members as cdm
INNER JOIN cd.bookings as cdb
ON cdb.memid = cdm.memid
INNER JOIN cd.facilities as cdf
ON cdf.facid = cdb.facid
WHERE DATE(cdb.starttime) = '2012-09-14'
AND ((cdb.memid = 0 AND cdf.guestcost * cdb.slots > 30) OR
    (cdb.memid <> 0 AND cdf.membercost * cdb.slots > 30)
  )
ORDER BY cost DESC;



## SQL practice
Retrieve a customer with the most rentals in 2017 year
![[Pasted image 20250615115437.png]]
## Create, Alter, and Drop Statements
![[Pasted image 20250617112806.png]]
![[Pasted image 20250617123345.png]]
![[Pasted image 20250617123539.png]]

![[Pasted image 20250617123432.png]]
In PostgreSQL, `bigserial` is a shorthand for creating an auto-incrementing column that uses the `BIGINT` data type. It automatically generates a unique, sequential integer for each new row added to the table. Essentially, `bigserial` combines a `BIGINT` column with an automatic sequence generator.
![[Pasted image 20250617124539.png]]
