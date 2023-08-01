# Difference between Prepared Statement and Statement in Java
 
 JDBC API provides 3 types of statements for wrapping an SQL query and sending for execution to the database.

1. **Statement**: It is used to execute normal SQL queries such as `select count(*) from Courses`. You can also use it to execute DDL, DML and DCL SQL statements. 
1. **Prepared Statement**: is specialized to execute parameterized queries such as `select * from Courses where courseId=?`, you can execute this SQL multiple times by just changing the course id parameters. They are compiled and cached at database end, hence quite fast for repeated execution.
1. **Callable Statement**: it is used to execute or call stored procedures stored in the database.

!!! info ""
	Each of the Statement class has a different purpose and you should use them for what they have designed for. It's very important to understand what they are and what is their purpose, along with how to use it correctly.

In this article, we will focus on understanding the difference between `Statement` and `Prepared Statement` by asking the below questions.


## 1. Which one to use and when?
Prepared Statement's sole purpose is to execute bind queries. If you need to execute a query multiple times with just different data then use `Prepared Statement` and use a placeholder, the question mark sign (?) for the variable data.

!!! question "Why it is called a prepared statement?" 
	When you first execute the prepared SQL query, the database will compile it and cache it for future reuse, next time you call the same query but with a different parameter, then the database will return the result almost immediately. *Because of this pre-compilation, this class is called Prepared Statement in Java.*

It's very useful to build search and insert queries e.g. if your application provides an interface to search some data such as course details, let's say by course, name, instructor, price, or topic. You can create `Prepared Statement` to handle that for better performance.

On the other hand, the sole purpose of `Statement` object is to execute a SQL query. You give them any query and it will execute it, but unlike `Prepared Statement`, it will not provide pre-compilation.


## 2. Syntax for these statements?
The syntax for `Statement` is same as SQL query, you can actually copy SQL from your favorite SQL editor and pass it as String to Statement for execution, but for `Prepared Statement`, you need to include placeholders i.e. questions mark (?) sign in SQL query e.g.

```sql
select count(*) from Books; 			//  Statement 
select * from Books where book_id=?; 	// Prepared Statement
```
The actual value is set before executing the query at runtime by using the various `setXXX()` methods e.g. if placeholder refers to a `varchar` column then you can use `setString(value)` to set the value. Similarly, if placeholder refers to an integer column then you can use `setInteger(value)` method.


## 3. Which has better performance?

 `Prepared Statement` provides better performance than `Statement` object because of pre-compilation of SQL query on the database server. This is because when you use Prepared Statement, the query is compiled the first time but after that it is cached at the database server, making subsequent run faster.

On the other hand, with the Statement object, even if you execute the same query again and again, they are always first compiled and then executed, making them slower compared to `Prepared Statement` queries.


## 4. Which one is more secure?

The `Prepared Statement` also provides safety against SQL injection, but the incorrect use of Statement can cause SQL injection. If you remember, the cause of SQL injection is malicious SQL code which is injected by malicious users. For example, you could have written above query which returns a book after passing Id as below:

```java
String id = getFromUser();
String SQL = "select * from Books where book_id=" + id;
```

If you pass this SQL to Statement object then it can cause SQL injection if a user sends malicious SQL code in form of id e.g.  `1 == 1` OR id, which will return every single book from the database. Though books, may not sound a sensitive data it could happen with any sensitive user data as well. `Prepared Statement` guards against this.


That's all about the difference between Statement and `Prepared Statement` in Java. You can use Statement to execute SQL queries but it's not recommended, especially if you can use `Prepared Statement`, which is more secure and fast approach to get the data from the database. If you have to pass parameters always use PreparedStatment, never create dynamic SQL queries by concatenating String, it's not safe and prone to SQL injection attack.
