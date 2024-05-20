## [Introduction to Java Servlets](https://www.geeksforgeeks.org/introduction-java-servlets/)

>[!info] Dynamic Web Pages
>Today, we all are aware of the need to create ***dynamic web pages*** i.e. the ones that can change the site contents according to the time or can generate the content according to the request received from the client.
>
>---
>
If you like coding in Java, then you will be happy to know that using Java there also exists a way to generate dynamic web pages and that way is ***Java Servlet***. 

---
## What is Java Servlet?

Java Servlets are the Java programs that run on the ==Java-enabled web server== or application server. They are used to handle the request obtained from the web server, process the request, produce the response, and then send a response back to the web server. 

#### Properties of Java Servlet
- Servlets work on the server side.
- Servlets are capable of handling complex requests obtained from the web server.

---
### Java Servlets Architecture

Servlet Architecture can be depicted from the image itself as provided below as follows:

![Servlets_architecture](https://media.geeksforgeeks.org/wp-content/uploads/20240305120707/Servlets_architecture-768.png)

---
### Execution of Java Servlets

Execution of Servlets basically involves Six basic steps: 

1. The Clients send the request to the Web Server.
2. The Web Server receives the request.
3. The Web Server passes the request to the corresponding Servlet.
4. The Servlet processes the request and generates the response in the form of output.
5. The Servlet sends the response back to the Web Server.
6. The Web Server sends the response back to the client and the client browser displays it on the screen.

---
### ***Need of Server-Side Extensions***

> [!info]
> The ***Server-Side Extensions*** are nothing but the technologies that are used to create dynamic Web pages.

Actually, to provide the facility of dynamic Web pages, ==Web pages need a container or Web server==.

>[!success] Servlet: an API to run in a Web Server
>To meet this requirement, ==independent Web server providers== offer some proprietary solutions in the form of **APIs*** (Application Programming Interface).   
>These ***APIs*** allow us to build programs that can run with a Web server.
>---
>***Java Servlet*** is one of the component APIs of ***Java Platform Enterprise Edition (nowdays known as – ‘Jakarta EE’)*** which sets standards for creating dynamic Web applications in Java.

Before learning about something, it’s important to know the need for that something, it’s not like that this is the only technology available for creating Dynamic Web Pages.

The Servlet technology is similar to other Web server extensions such as:
1. ***Common Gateway Interface*** (CGI) scripts
2. ***Hypertext Preprocessor*** (PHP).

However, Java Servlets are more acceptable since they solve the limitations of ***CGI*** such as low performance and low degree scalability.  

---
## ***CGI - Common Gateway Interface***

***CGI*** is actually an external application that is written by using any of the programming languages like ***C*** or ***C++*** and this is responsible for processing client requests and generating dynamic content. 


In CGI application, when a client makes a request to access dynamic Web pages, the Web server performs the following operations:  
- It first locates the requested web page __i.e__ the required CGI application using URL.
- It then creates a new process to service the client’s request.
- Invokes the CGI application within the process and passes the request information to the application.
- Collects the response from the CGI application.
- Destroys the process, prepares the HTTP response, and sends it to the client.


![CGI](https://media.geeksforgeeks.org/wp-content/uploads/20240305125247/CGI-768.png)

>[!warning]
>So, in ***CGI*** server has to create and destroy the process for every request.
>It’s easy to understand that this approach is applicable for handling few clients but as the number of clients increases, the workload on the server increases and so the time is taken to process requests increases.

---
##### ***Reference***
- [Geeks 4 Geeks article](https://www.geeksforgeeks.org/introduction-java-servlets/)