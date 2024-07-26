> [!info] The JDBC API consists of a set of interfaces and classes written in the Java programming language.
> [Java Database Connectivity](https://www.ibm.com/docs/en/informix-servers/12.10?topic=started-what-is-jdbc) is the JavaSoft specification of a standard API that allows Java programs to access database management systems.

Using these standard interfaces and classes, programmers can write applications that connect to databases, send queries written in structured query language (SQL), and process the results.

Since JDBC is a standard specification, one Java program that uses the JDBC API can connect to any ==Database Management System== (DBMS), as long as a driver exists for that particular DBMS.

---
## JDBC Driver

The JDBC API defines the Java™ interfaces and classes that programmers use to connect to databases and send queries. 

> A JDBC driver implements these interfaces and classes for a particular DBMS vendor.

A Java program that uses the JDBC API loads the specified driver for a particular DBMS before it actually connects to a database.
The JDBC **DriverManager** class then sends all JDBC API calls to the loaded driver.

> [!info] There are four types of JDBC drivers:
> 
>##### Type 1 driver - JDBC-ODBC bridge plus ODBC driver
   Translates JDBC API calls into ==Microsoft ODBC== calls that are then passed to the ODBC driver
   The ODBC binary code must be loaded on every client computer that uses this type of driver.
   ODBC is an acronym for Open Database Connectivity.
   >
>##### Type 2 driver: Native-API, partly Java driver
   Converts JDBC API calls into DBMS-specific client API calls
   Like the bridge driver, this type of driver requires that some binary code is loaded on each client computer.
   >
>##### Type 3 driver: JDBC-Net, pure-Java driver
   Sends JDBC API calls to a middle-tier server that translates the calls into the DBMS-specific network protocol
   The translated calls are then sent to a particular DBMS.
   >
>##### Type 4 driver: Native-protocol, pure-Java driver
   Converts JDBC API calls directly into the DBMS-specific network protocol without a middle tier

This driver allows the client applications to connect directly to the database server.

---
##### References
- [IBM doc](https://www.ibm.com/docs/en/informix-servers/12.10?topic=started-what-is-jdbc)
- 