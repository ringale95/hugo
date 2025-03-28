+++
date = '2025-02-14T21:12:53-05:00'
draft = true
title = 'Database management and Database Design'
+++
## Normalization in relational database design.

As part of DAMG6210 Database Management & Database Design, this post highlights the necessary aspects of normalizing your dataset.

## Why to normalize a database?
Normalization is a process in database design that organizes data to minimize redundancy and dependency. It helped to solve below problems in database:
- Update Anomaly
  - Modification Anomalies 
    - If data is repeated it will become inconsistent to update data everywhere
  - Deletion Anomalies
    - If we delete a record to remove a piece of information, we might as a consequence lose some additional information
  - Insertion Anomalies
    - If we don't have information about primary key we might not be able to insert the data

![alt](/image.png)

This table has potential update problems
- Rows are repeated which can lead to inconsistent data in future
- Primary key in this table is combination of (empID, proj_num) . There is a problem if we want to keep an information about project but there is no employee yet working on it we have no value for empId that means primary key will be null
- There is deletion issue if  I try to remove a project the employee will also be removed

### Solution to above problems?

Split this table into two one to record projects and another employees.

## Functional Dependencies
A functionally dependent means `If I know value for this attribute, I can uniquely tell you value of some other attribute`.

Example:
If I know value of employee ID, I can tell you his last name. 
If I know value of empID, I cannot tell you his unique project number

## Primary Keys
If I know the value of key, I can tell you value of every other field in the row. `last_name `cannot be a key field

A primary key must not have unnecessary fields. (empID, last_name) can be a key but last_name is unnecessary we can still find the row with empID

## Normalization forms

### First normal form

    - Any multivalued attributes (repeating groups) is removed.
    - Single value in every cell

Example:
![alt](/1NFFail.png)

Here, In `Courses` column there are two values in each row. Divide those into different rows

### Second normal form
Any partial dependencies in composite key are removed. All non-key attributes are dependent on primary key

![alt](/2NFFAil.png)

In this Primary Key = (Student_ID, Course_ID)
Student_Name dependends on Student_ID
Course_Name and Instructors are dependent on Course_ID

So not all the values are dependent on both, In this case take out those who are partially dependent

![alt](/2NFCorrect.png)

Example 2:
![alt](/2NFEx.png)

We create different table:
- Order_ID, Customer_ID, Payment_Details
- Customer_ID, Customer_Name, Address
- Order_ID, Product_ID, Qty, total_amt
- Product_ID, Product_name


#### Ask below questions?
- What is primary key?
  - Should not repeat (if it does go with composite key). If composite key is there then work for second normal form
  - No null value
- Check for any partial dependencies

### Third Normal Form

Third normal form is achieved by:
- It is in 2NF. 
  - This means all non-key attributes are fully dependent on the entire primary key (no partial dependencies).
- It has no transitive dependencies.
    - A transitive dependency occurs when a non-key attribute depends indirectly on primary key and not directly
Remove all ones from the table who are dependent on another ID