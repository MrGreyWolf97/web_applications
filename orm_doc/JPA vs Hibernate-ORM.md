### [Overview of ORM layer](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#overview-of-orm-layer)

[Object Relational Mapping](https://www.theserverside.com/definition/object-relational-mapping-ORM#:~:text=Object%2Drelational%20mapping%20(ORM)%20is%20a%20way%20to%20align,language%20and%20a%20relational%20database.) (ORM) in simple terms is mapping our application objects to tables in our database using object-oriented programming.

We achieve interaction with our various relational databases using ORM, to fetch or retrieve our information without writing native SQL.

The vast majority of Java-based or any applications hosted on the internet need either the developers or the end-users to perform database operations, such as creating, retrieving, updating, and deleting a large amount of data.

We can all agree that performing these database operations can sometimes be very tedious.

As you can see from the Java Database Connectivity (JDBC) library, it requires writing a lot of boilerplate lines of code.

So to minimize or lessen the burden of writing these codes to interact with the database, Java-enabled tools called [Hibernate](https://www.javatpoint.com/hibernate-tutorial) and [Java Persistence API](https://www.javatpoint.com/jpa-introduction) (JPA) have been provided as industrial standardized options, which can be substituted in place of JDBC or writing native SQL syntax to interact with our databases.

Let’s go further and explore the concepts of JPA and Hibernate.

### [What is JPA?](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#what-is-jpa)
Have you ever wondered what enables the interaction between our Java applications and databases? I guess you do now. This is all made possible by the Java Persistence API. JPA provides and defines the specifications for persisting, accessing, and managing data between Java objects (POJO or Entity) and relational databases.

### [What is Hibernate?](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#what-is-hibernate)
As the popular saying goes “Nobody is an island”, you need others to survive. Both Hibernate and JPA need each other. Hibernate-ORM is one of the most popular implementations of JPA. It helps to map Java objects to database tables. What Hibernate does under the hood, is to translate Java codes into SQL queries that the DBMS (Database Management System) can understand. Let’s look at the illustration, which shows the mapping of an Entity to a Database table.

Hibernate ORM Mapping:

![An graphical representation of mapping an object or class entity to a relational database through Hibernate](https://miro.medium.com/v2/resize:fit:421/1*DiktbvdVxqTnd_iMIggFbQ.png)

Right now, you have gotten pretty familiar with what JPA and Hibernate are all about. Let’s look into the key differences

### [Key differences between JPA and Hibernate](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#key-differences-between-jpa-and-hibernate)

- From the discussion we have had thus far, it is pretty obvious that JPA is a mere specification for managing the database. JPA has no implementation, as it is a guideline to follow to manipulate our database. On the other, Hibernate is the implementation of the JPA specification. Hibernate is the code implementation that meets the API as defined by the JPA specification.
- In simple terms, JPA can be called the interface, while Hibernate is the implementation of these interfaces.
- JPA specifies standards for developers to perform database operations seamlessly, while Hibernate uses these standards of the Java Persistence API to carry out operations on the database.
- It is also worth knowing that JPA has its native query language called Java Persistence Query Language (JPQL), which is an object-oriented query language to perform database operations. On the other hand, Hibernate uses HQL (Hibernate Query Language), which is also an object-oriented query language to perform database operations.

### [Relationship between JPA and Hibernate](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#relationship-between-jpa-and-hibernate)
As we have established that fact that JPA defines the specifications that Hibernate implements. This implies that to maintain the relationship between the two, Hibernate must adhere to the rules made available by the JPA specification. We can also deduce that JPA provides a standardized mechanism for Java applications to connect with a DBMS via Hibernate or any other JPA implementation. It abstracts away many of the low-level details of database administration. Let’s look at the diagram below.

Communication between JPA and Hibernate:

![Communication taking place between JPA and Hibernate](https://miro.medium.com/v2/resize:fit:700/1*S_vZOWfmkl0iZt8D7YjEUQ.png)

You can see from the basic illustration that our Java program communicates with the JPA interface. The Hibernate implementation is communicated using the JPA interface. Hibernate converts Java objects into SQL queries, which it then sends to the database. The database executes the SQL queries and returns the results to Hibernate (if need be). Hibernate returns the results to your Java application in the form of Java objects.

### [Conclusion](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#conclusion)
In this article, you have been able to dive into Object Relational Mapping, key concepts of Java Persistence API, and Hibernate. Also, we discussed the key differences between the two concepts, where JPA is a Java standard that specifies how Java programs should connect with databases, and one of the numerous implementations of this specification is Hibernate. It serves as a link between your Java application and the database, converting Java objects to SQL queries.


---
##### References
- [StackCademy](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad)
- 