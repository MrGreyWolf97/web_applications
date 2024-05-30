> [!question] [how to modify web.xml for multiple servlet](https://stackoverflow.com/questions/43559372/how-to-modify-web-xml-for-multiple-servlet)
> I just get confused about how to modify `web.xml` for multiple servlet.
> I got three servlet to handle three different JSP, but now only one servlet is effective.

You should declare and define the classes/servlets inside the web.xml file like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee                                 
         http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
    
    <servlet>
        <servlet-name>LoginForm</servlet-name>
        <servlet-class>com.project.system.LoginForm</servlet-class>
    </servlet>
    <servlet>
        <servlet-name>RegisterForm</servlet-name>
        <servlet-class>com.project.system.RegisterForm</servlet-class>
    </servlet>
    <servlet>
        <servlet-name>UserController</servlet-name>
        <servlet-class>com.project.controller.UserController</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>LoginForm</servlet-name>
        <url-pattern>/loginForm</url-pattern>
    </servlet-mapping>   
    <servlet-mapping>
        <servlet-name>RegisterForm</servlet-name>
        <url-pattern>/registerForm</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>UserController</servlet-name>
        <url-pattern>/userController</url-pattern>
    </servlet-mapping>

    <session-config>
        <session-timeout>
            30
        </session-timeout>
    </session-config>

</web-app>
```

---
##### ***References***
- [StackOverflow post](https://stackoverflow.com/questions/43559372/how-to-modify-web-xml-for-multiple-servlet)
- 