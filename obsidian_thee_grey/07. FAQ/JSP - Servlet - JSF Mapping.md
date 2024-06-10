 >[!question] [What is the difference between creating JSF pages with .jsp or .xhtml or .jsf extension](https://stackoverflow.com/questions/7914660/what-is-the-difference-between-creating-jsf-pages-with-jsp-or-xhtml-or-jsf-ex)
 >I saw some examples creating the JSF pages with `.jsp` extension, other examples creating them with `.xhtml` extension, and other examples choose `.jsf`. I just would like to know what the difference is between above extensions when working with JSF pages, and how to choose the appropriate extension?
 
 - JSP is an old view technology and widely used in combination with JSF 1.x.
 - Facelets (by some people overgeneralized as [XHTML](https://stackoverflow.com/tags/xhtml/info)) is the successor of JSP and introduced as default view technology of JSF 2.x at end of 2009.

 When you were seeing JSPs, you were perhaps reading outdated books, tutorials or resources targeted on JSF 1.x.
 You should generally ignore them when developing with JSF 2.x and head to resources targeted on JSF 2.x, otherwise you may end up in confusion because many things are done differently in JSF 2.x on Facelets.

>[!info] Extensions
>
>> [!success] The `*.jsf` is just one of widely used URL patterns of the `FacesServlet` mapping in `web.xml`.
>
>>[!warning] Other ones are `*.faces` and `/faces/*`, but those are from back in the JSF 1.0/1.1 ages.
>
> They all do not represent the concrete file extension/path, but just a virtual file extension/path and is to be specified in URLs only like so:
>
>`http://example.com/contextname/page.jsf`
> 
> If you are familiar with basic [Servlets](https://stackoverflow.com/tags/servlets/info), then you should know that the ==Servlet Container== will invoke the servlet when the request URL matches the servlet's URL pattern.

So when the request URL matches `*.jsf`, then the `FacesServlet` will be invoked this way.
When using JSPs, it would actually execute `page.jsp`.
When using Facelets, this would actually compile `page.xhtml`.

Since JSF 2.x you can also use `*.xhtml` as URL pattern. This way you don't need to get confused when specifying URLs.
Using `*.xhtml` as URL pattern was not possible in JSF 1.x with Facelets 1.x, because the `FacesServlet` would then run in an infinite loop calling itself every time.
An additional advantage of using `*.xhtml` is that the end-user won't be able to see raw JSF source code whenever the end-user purposefully changes the URL extension in browser address bar from for example `.jsf` to `.xhtml`.
It is not possible to use `*.jsp` as URL pattern, because this way the container's built-in `JspServlet`, which is already using that URL pattern, would be overridden and then the `FacesServlet` wouldn't be able to feed on JSPs anymore.

---
### From the Spec

`.jsp` files are generally used for JSF views defined using ==JavaServer Pages==. 
`.xhtml` files are generally used for JSF views defined using ==Facelets==.

This can be changed via configuration (e.g. see the `javax.faces.DEFAULT_SUFFIX` and `javax.faces.FACELETS_SUFFIX` configuration parameters.)

Other extension mappings (`*.jsf`, `*.faces`) tend to be used for processing requests via the `FacesServlet`.
This is a logical mapping to the view which the JSF runtime will handle. How mappings are handled is defined in the `web.xml` (that doesn't have to be done using extensions; the `/faces/*` mapping is often used.

From the spec:

> # Servlet Mapping
> 
> All requests to a web application are mapped to a particular servlet based on matching a URL pattern (as defined in the Java Servlet Specification) against the portion of the request URL after the context path that selected this web application.
> 
> JSF implementations must support web application that define a `<servlet-mapping>` that maps any valid url-pattern to the FacesServlet.
> Prefix or extension mapping may be used.
> When using prefix mapping, the following mapping is recommended, but not required:
>
> ```xml
><servlet-mapping>
><servlet-name> faces-servlet-name </servlet-name>
><url-pattern>/faces/*</url-pattern>
></servlet-mapping>
>```
> 
> When using extension mapping the following mapping is recommended, but not required:
> 
> ```xml
> <servlet-mapping>
> <servlet-name> faces-servlet-name </servlet-name>
> <url-pattern>*.faces</url-pattern>
> </servlet-mapping>
> ```
> 
> In addition to FacesServlet, JSF implementations may support other ways to invoke the JavaServer Faces request processing lifecycle, but applications that rely on these mechanisms will not be portable.

---
### See also:

- [What is the difference between JSF, Servlet and JSP?](https://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp)
- [Why Facelets is preferred over JSP as the view definition language from JSF2.0 onwards?](https://stackoverflow.com/questions/13092161/why-facelets-is-preferred-over-jsp-as-the-view-definition-language-from-jsf2-0-o/)
- [JSF Facelets: Sometimes I see the URL is .jsf and sometimes .xhtml. Why?](https://stackoverflow.com/questions/3008395/jsf-facelets-sometimes-i-see-the-url-is-jsf-and-sometimes-xhtml-why)

---
##### ***References***
- [StackOverflow post](https://stackoverflow.com/questions/7914660/what-is-the-difference-between-creating-jsf-pages-with-jsp-or-xhtml-or-jsf-ex)
- 