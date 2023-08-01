# Manipulating Tables with Delta Lake

This notebook provides a hands-on review of some of the basic functionality of Delta Lake.

## Learning Objectives
By the end of this lab, you should be able to:
- Execute standard operations to create and manipulate Delta Lake tables, including:
  - **`CREATE TABLE`**
  - **`INSERT INTO`**
  - **`SELECT FROM`**
  - **`UPDATE`**
  - **`DELETE`**
  - **`MERGE`**
  - **`DROP TABLE`**

## Setup
Run the following script to setup necessary variables and clear out past runs of this notebook. Note that re-executing this cell will allow you to start the lab over.

```bash
%run ../Includes/Classroom-Setup-2.2L
```


## Create a Table

In this notebook, we'll be creating a table to track our bean collection.

Use the cell below to create a managed Delta Lake table named **`beans`**.

Provide the following schema:

| Field Name | Field type |
| --- | --- |
| name | STRING |
| color | STRING |
| grams | FLOAT |
| delicious | BOOLEAN |


```sql
create table beans 
(name string, color string, grams float, delicious boolean)
```

!!! note "Note"

     We'll use Python to run checks occasionally throughout the lab. The following cell will return as error with a message on what needs to change if you have not followed instructions. No output from cell execution means that you have completed this step.

```python
assert spark.table("beans"), "Table named `beans` does not exist"
assert spark.table("beans").columns == ["name", "color", "grams", "delicious"], "Please name the columns in the order provided above"
assert spark.table("beans").dtypes == [("name", "string"), ("color", "string"), ("grams", "float"), ("delicious", "boolean")], "Please make sure the column types are identical to those provided above"
```


## Insert Data

Run the following cell to insert three rows into the table.

```SQL
INSERT INTO beans VALUES
("black", "black", 500, true),
("lentils", "brown", 1000, true),
("jelly", "rainbow", 42.5, false)
```


Manually review the table contents to ensure data was written as expected.

```sql
select * from beans
```

Insert the additional records provided below. Make sure you execute this as a single transaction.

```sql
insert into beans values
('pinto', 'brown', 1.5, true),
('green', 'green', 178.3, true),
('beanbag chair', 'white', 40000, false)
```

Run the cell below to confirm the data is in the proper state.

```python
assert spark.conf.get("spark.databricks.delta.lastCommitVersionInSession") == "2", "Only 3 commits should have been made to the table"
assert spark.table("beans").count() == 6, "The table should have 6 records"
assert set(row["name"] for row in spark.table("beans").select("name").collect()) == {'beanbag chair', 'black', 'green', 'jelly', 'lentils', 'pinto'}, "Make sure you have not modified the data provided"
```
## Update Records

A friend is reviewing your inventory of beans. After much debate, you agree that jelly beans are delicious.

Run the following cell to update this record.


```sql
UPDATE beans
SET delicious = true
WHERE name = "jelly"
```

You realize that you've accidentally entered the weight of your pinto beans incorrectly.

Update the **`grams`** column for this record to the correct weight of 1500.


```sql
update beans 
set grams = 1500
where name = 'pinto'
```

Run the cell below to confirm this has completed properly.

```python
assert spark.table("beans").filter("name='pinto'").count() == 1, "There should only be 1 entry for pinto beans"
row = spark.table("beans").filter("name='pinto'").first()
assert row["color"] == "brown", "The pinto bean should be labeled as the color brown"
assert row["grams"] == 1500, "Make sure you correctly specified the `grams` as 1500"
assert row["delicious"] == True, "The pinto bean is a delicious bean"
```

## Delete Records

You've decided that you only want to keep track of delicious beans.

Execute a query to drop all beans that are not delicious.


```sql
delete from beans
where delicious = false
```


Run the following cell to confirm this operation was successful.

```python
assert spark.table("beans").filter("delicious=true").count() == 5, "There should be 5 delicious beans in your table"
assert spark.table("beans").filter("delicious=false").count() == 0, "There should be 0 delicious beans in your table"
assert spark.table("beans").filter("name='beanbag chair'").count() == 0, "Make sure your logic deletes non-delicious beans"
```

## Using Merge to Upsert Records

Your friend gives you some new beans. The cell below registers these as a temporary view.

```sql
CREATE OR REPLACE TEMP VIEW new_beans(name, color, grams, delicious) AS VALUES
('black', 'black', 60.5, true),
('lentils', 'green', 500, true),
('kidney', 'red', 387.2, true),
('castor', 'brown', 25, false);


SELECT * FROM new_beans
```

In the cell below, use the above view to write a merge statement to update and insert new records to your **`beans`** table as one transaction.

Make sure your logic:
- Matches beans by name **and** color
- Updates existing beans by adding the new weight to the existing weight
- Inserts new beans only if they are delicious


```sql
merge into beans a
using new_beans b
on a.name= b.name and a.color = b.color
when matched then 
update set grams = a.grams + b.grams
when not matched and b.delicious = true then
insert *
```

Run the cell below to check your work.

```python
version = spark.sql("DESCRIBE HISTORY beans").selectExpr("max(version)").first()[0]
last_tx = spark.sql("DESCRIBE HISTORY beans").filter(f"version={version}")
assert last_tx.select("operation").first()[0] == "MERGE", "Transaction should be completed as a merge"
metrics = last_tx.select("operationMetrics").first()[0]
assert metrics["numOutputRows"] == "3", "Make sure you only insert delicious beans"
assert metrics["numTargetRowsUpdated"] == "1", "Make sure you match on name and color"
assert metrics["numTargetRowsInserted"] == "2", "Make sure you insert newly collected beans"
assert metrics["numTargetRowsDeleted"] == "0", "No rows should be deleted by this operation"
```

## Dropping Tables

When working with managed Delta Lake tables, dropping a table results in permanently deleting access to the table and all underlying data files.

**NOTE**: Later in the course, we'll learn about external tables, which approach Delta Lake tables as a collection of files and have different persistence guarantees.

In the cell below, write a query to drop the **`beans`** table.

```sql
drop table beans
```


Run the cell below to assert that your table no longer exists.
```python
assert spark.sql("SHOW TABLES LIKE 'beans'").collect() == [], "Confirm that you have dropped the `beans` table from your current database"
```

