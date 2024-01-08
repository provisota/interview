# Scope
1. ORM (Object-Relational Mapping):
    - ORM is a programming technique for converting data between incompatible type systems using object-oriented programming languages. This creates a "virtual object database" that can be used from within the programming language. There are both free and commercial packages available that perform object-relational mapping, although some programmers opt to construct their own ORM tools.

2. Hibernate, SpringData, JPA:
    - Hibernate: Hibernate ORM is an object-relational mapping tool for the Java programming language. It provides a framework for mapping an object-oriented domain model to a relational database. Hibernate handles object-relational impedance mismatch problems by replacing direct, persistent database accesses with high-level object handling functions.

    ```java
    @Entity
    public class Employee {
        @Id
        @GeneratedValue
        private Long id;
        private String name;
        private String department;
        // getters and setters
    }
    ```

    - Spring Data: Spring Data’s mission is to provide a familiar and consistent, Spring-based programming model for data access while still retaining the special traits of the underlying data store. It makes it easy to use data access technologies, relational and non-relational databases, map-reduce frameworks, and cloud-based data services.

    ```java
    public interface EmployeeRepository extends CrudRepository<Employee, Long> {
        List<Employee> findByName(String name);
    }
    ```

    - JPA (Java Persistence API): JPA is a Java application programming interface specification that describes the management of relational data in applications using Java Platform, Standard Edition and Java Platform, Enterprise Edition. It provides a way to map between Java objects and relational database tables.

    ```java
    @Entity
    public class Employee {
        @Id
        @GeneratedValue
        private Long id;
        private String name;
        private String department;
        // getters and setters
    }
    ```
# Questions
1. What is the object-relational mapping?
2. What is the Java Persistence API?
3. What is HQL (Hibernate Query Language)?
4. What is lazy loading in hibernate? (Note: In case candidate did not work with it ask how to load linked collection of one to many items )
5. What is pessimistic and optimistic locking?
6. What is Spring Data? (Note: In case candidate have not worked with Spring Data please ask how application data layer was implemented in his/her  previous projects)
7. What is the difference between first level cache and second level cache? (Note: This question is bounded to Hibernate. In case candidate has not hadan experiece with it please ask how to implement read through cache in application memory and how to move the cache storage out of applicationl)
8. What alternatives to ORM do you know?
# Answers
1. Object-Relational Mapping (ORM) is a programming technique that allows you to interact with your database, like you would with SQL. In other words, it allows you to manipulate your data as objects. This removes the need for most of the data-access code that developers usually need to write.

2. The Java Persistence API (JPA) is a Java specification that provides certain functionality and standards to ORM tools. It describes the management of relational data in applications using Java Platform, Standard Edition and Java Platform, Enterprise Edition.

3. Hibernate Query Language (HQL) is an object-oriented query language, similar to SQL, but it operates on objects, properties and classes. While SQL operates on database tables, columns and rows.

4. Lazy loading is a design pattern which is used to defer initialization of an object until the point at which it is needed. In Hibernate, it's used to delay the loading of child entities from the database until you access them. For example, if you have an entity `Person` with many `Address` entities, those addresses won't be loaded from the database until you call `person.getAddresses()`.

5. Pessimistic locking is where you lock the record for your exclusive use until you have finished with it. It has much better integrity than optimistic locking but requires you to be careful with your application design to avoid Deadlocks. On the other hand, optimistic locking is where you check if the record was changed by someone else before you commit your changes. It's used when you don't expect many conflicts and don't want to lock the records.

6. Spring Data’s mission is to provide a familiar and consistent, Spring-based programming model for data access while still retaining the special traits of the underlying data store. It simplifies the creation of a Repository by providing CRUD operations on your Entity.

7. First-level cache is associated with the `Session` object, while second-level cache is associated with the `SessionFactory` object. By default, Hibernate uses first-level cache on a per-transaction basis. Hibernate uses this cache mainly to reduce the number of SQL queries it needs to generate within a given transaction. For example, if an object is modified several times within the same transaction, Hibernate will generate only one SQL UPDATE statement at the end of the transaction, containing all the modifications.

8. Alternatives to ORM include:
    - SQL Query Builders like jOOQ or MyBatis.
    - Database-specific abstraction layers like Spring's `JdbcTemplate`.
    - Micro-ORMs like Dapper or Massive.
    - NoSQL databases, which don't require a mapping between the database and the object model.