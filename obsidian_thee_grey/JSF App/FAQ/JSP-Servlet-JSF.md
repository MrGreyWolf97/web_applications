> [!question] [What is the difference between JSF, Servlet and JSP?](https://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp)
>
> I have some questions.
> These are :
>1. How are JSP and Servlet related to each other?
>2. Is JSP some kind of Servlet?
>3. How are JSP and JSF related to each other?
>4. Is JSF some kind of **Pre-Build UI based JSP** like ASP.NET-MVC?

---
### [JSP (JavaServer Pages)](https://stackoverflow.com/tags/jsp/info)

JSP is a **Java view technology** running on the server machine which allows you to write template text in client side languages (like HTML, CSS, JavaScript, ect.).
JSP supports [taglibs](http://docs.oracle.com/javaee/5/tutorial/doc/bnann.html), which are backed by pieces of Java code that let you control the page flow or output dynamically.
A well-known taglib is [JSTL](https://stackoverflow.com/tags/jstl/info).
JSP also supports [Expression Language](https://stackoverflow.com/tags/el/info), which can be used to access backend data (via attributes available in the page, request, session and application scopes), mostly in combination with taglibs.

When a JSP is requested for the first time or when the web app starts up, the servlet container will compile it into a class extending [`HttpServlet`](http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServlet.html) and use it during the web app's lifetime.
You can find the generated source code in the server's work directory.
In for example [Tomcat](http://tomcat.apache.org), it's the `/work` directory.
On a JSP request, the servlet container will execute the compiled JSP class and send the generated output (usually just HTML/CSS/JS) through the web server over a network to the client side, which in turn displays it in the web browser.

>[!tip] JSP
>JSP is built on top of servlets and provides a simpler, page-based solution to generating large amounts of dynamic HTML content for Web user interfaces.
>JavaServer Pages enables Web developers and designers to simply edit HTML pages with special tags for the dynamic, Java portions.
>JavaServer Pages works by having a special servlet known as a JSP container, which is installed on a Web server and handles all JSP page view requests.
>The JSP container translates a requested JSP into servlet code that is then compiled and immediately executed.
>Subsequent requests to the same page simply invoke the runtime servlet for the page.
>If a change is made to the JSP on the server, a request to view it triggers another translation, compilation, and restart of the runtime servlet.

---
### [Servlets](https://stackoverflow.com/tags/servlets/info)

Servlet is a **Java application programming interface (API)** running on the server machine, which intercepts requests made by the client and generates/sends a response. A well-known example is the `HttpServlet` which provides methods to hook on [HTTP](http://www.w3.org/Protocols/rfc2616/rfc2616.html) requests using the popular [HTTP methods](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) such as `GET` and `POST`.
You can configure `HttpServlet`s to listen to a certain HTTP URL pattern, which is configurable in `web.xml`, or more recently with [Java EE 6](http://docs.oracle.com/javaee/6/tutorial/doc/bnafd.html), with `@WebServlet` annotation.

When a Servlet is first requested or during web app startup, the servlet container will create an instance of it and keep it in memory during the web app's lifetime. The same instance will be reused for every incoming request whose URL matches the servlet's URL pattern. You can access the request data by [`HttpServletRequest`](http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletRequest.html) and handle the response by [`HttpServletResponse`](http://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpServletResponse.html). Both objects are available as method arguments inside any of the overridden methods of `HttpServlet`, such as `doGet()` and `doPost()`.

>[!tip] Servlets
>The Java Servlet API enables Java developers to write server-side code for delivering dynamic Web content.
>Like other proprietary Web server APIs, the Java Servlet API offered improved performance over CGI; however, it has some key additional advantages.
>Because servlets were coded in Java, they provides an object-oriented (OO) design approach and, more important, are able to run on any platform.
>Thus, the same code was portable to any host that supported Java.
>Servlets greatly contributed to the popularity of Java, as it became a widely used technology for server-side Web application development.

---
### [JSF (JavaServer Faces)](https://stackoverflow.com/tags/jsf/info)

JSF is a **component based MVC framework** which is built on top of the Servlet API and provides [components](http://docs.oracle.com/javaee/6/tutorial/doc/bnarf.html) via taglibs which can be used in JSP or any other Java based view technology such as [Facelets](http://docs.oracle.com/javaee/6/tutorial/doc/giepx.html). Facelets is much more suited to JSF than JSP. It namely provides great [templating capabilities](http://docs.oracle.com/javaee/6/tutorial/doc/giqxp.html) such as [composite components](http://docs.oracle.com/javaee/6/tutorial/doc/giqzr.html), while JSP basically only offers the [`<jsp:include>`](http://java.sun.com/products/jsp/syntax/2.0/syntaxref2020.html#8828) for templating in JSF, so that you're forced to create custom components with raw Java code (which is a bit opaque and a lot of tedious work) when you want to replace a repeated group of components with a single component. Since JSF 2.0, JSP has been deprecated as view technology in favor of Facelets.

**Note**: JSP itself is NOT deprecated, just the combination of JSF with JSP is deprecated.

**Note**: JSP has great templating abilities by means of Taglibs, especially the ([Tag File](http://docs.oracle.com/javaee/5/tutorial/doc/bnann.html)) variant. JSP templating in combination with JSF is what is lacking.

As being a MVC ([Model-View-Controller](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)) framework, JSF provides the [`FacesServlet`](http://docs.oracle.com/javaee/6/api/javax/faces/webapp/FacesServlet.html) as the sole request-response _Controller_. It takes all the standard and tedious HTTP request/response work from your hands, such as gathering user input, validating/converting them, putting them in model objects, invoking actions and rendering the response. This way you end up with basically a JSP or Facelets (XHTML) page for _View_ and a JavaBean class as _Model_. The JSF components are used to bind the view with the model (such as your ASP.NET web control does) and the `FacesServlet` uses the _JSF component tree_ to do all the work.

>[!tip] JSF
>JavaServer Faces is a standard Java framework for building user interfaces for Web applications.
>Most important, it simplifies the development of the user interface, which is often one of the more difficult and tedious parts of Web application development. 
>Although it is possible to build user interfaces by using foundational Java Web technologies (such as ==Java Servlets and JavaServer Pages==) without a comprehensive framework designed for enterprise Web application development, these core technologies can often lead to a variety of development and maintenance problems.
>More important, by the time the developers achieve a production-quality solution, the same set of problems solved by JSF will have been solved in a nonstandard manner.
>---
>JavaServer Faces is designed to simplify the development of user interfaces for Java Web applications in the following ways:
>- It provides a component-centric, client-independent development approach to building Web user interfaces, thus improving developer productivity and ease of use.
>- It simplifies the access and management of application data from the Web user interface.
>- It automatically manages the user interface state between multiple requests and multiple clients in a simple and unobtrusive manner.
>- It supplies a development framework that is friendly to a diverse developer audience with different skill sets.
>- It describes a standard set of architectural patterns for a web application.

---
# Related questions

- [What is the main-stream Java alternative to ASP.NET / PHP?](https://stackoverflow.com/questions/2556553/what-is-the-main-stream-java-alternative-to-asp-net-php)
- [Java EE web development, what skills do I need?](https://stackoverflow.com/questions/1958808/java-web-development-what-skills-do-i-need)
- [How do servlets work? Instantiation, session variables and multithreading](https://stackoverflow.com/questions/3106452/java-servlet-instantiation-and-session-variables)
- [What is a Javabean and where are they used?](https://stackoverflow.com/questions/1727603/places-where-java-beans-used)
- [How to avoid Java code in JSP files?](https://stackoverflow.com/questions/3177733/howto-avoid-java-code-in-jsp-files)
- [What components are MVC in JSF MVC framework?](https://stackoverflow.com/questions/5104094/what-components-are-mvc-in-jsf-mvc-framework)
- [What is the need of JSF, when UI can be achieved with JavaScript libraries such as jQuery and AngularJS](https://stackoverflow.com/questions/4421839/what-is-the-need-of-jsf-when-ui-can-be-achieved-from-css-html-javascript-jquery/)

---
##### **References***
- [StackOverflow post](https://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp)
- 