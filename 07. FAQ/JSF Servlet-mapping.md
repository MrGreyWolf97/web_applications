>[!question] [Sometimes I see JSF URL is *.jsf, sometimes *.xhtml and sometimes /faces/*. Why?](https://stackoverflow.com/questions/3008395/sometimes-i-see-jsf-url-is-jsf-sometimes-xhtml-and-sometimes-faces-why)
>
>Been try to learn JSF, and sometimes I see the URL is `*.jsf` and sometimes is `*.xhtml` or `/faces/*`.
>Can someone fill my knowledge, please?
>When I create a JSF using Facelet, the file extension is `.xhtml`, so where does `.jsf` URL extension come from?

The `.jsf` extension is where the `FacesServlet` is during the JSF 1.2 period often mapped on in the `web.xml`.

```xml
<servlet-mapping>
    <servlet-name>facesServlet</servlet-name>
    <url-pattern>*.jsf</url-pattern>
</servlet-mapping>
```

> [!success] The `.xhtml` extension is of the **actual** Facelets file as you've physically placed in the `webcontent` of your `webapp`, e.g. `Webapp/WebContent/page.xhtml`.

If you invoke this page with the `.jsf` extension, e.g. `http://localhost:8080/webapp/page.jsf` then the `FacesServlet` will be invoked, locate the `page.xhtml` file and parse/render its JSF components. If the `FacesServlet` isn't invoked, then the end-user would end up getting the raw XHTML source code (which can be seen by right-click, _View Source_).

Sometimes a `*.faces` extension or `/faces/*` folder-mapping is been used.
But this was from back in the JSF 1.0/1.1 ages. You're free to choose and use whatever mapping you'd like to let `FacesServlet` listen on, even if it's a nothing-saying `*.xyz`. The actual page itself should always have the `.xhtml` extension, but this is configurable by the following `<context-param>` in `web.xml`:

```xml
<context-param>
    <param-name>javax.faces.DEFAULT_SUFFIX</param-name>
    <param-value>.xml</param-value>
</context-param>
```

This will change the `FacesServlet` to locate `page.xml` instead of (default) `page.xhtml`.

More recently, with JSF/Facelets 2.0 a `*.xhtml` mapping is been used.
In JSF/Facelets 1.x it was not possible to use the same mapping extension as the physical file. It would result in an infinite loop. But since JSF/Facelets 2.0 it is possible and this allows you to call the page by `http://localhost:8080/webapp/page.xhtml`.

```xml
<servlet-mapping>
    <servlet-name>facesServlet</servlet-name>
    <url-pattern>*.xhtml</url-pattern>
</servlet-mapping>
```

This way you don't need to configure some security restrictions to hide the raw source files away for cases whenever the end-user changes for example `.jsf` in URL to `.xhtml` in browser address bar.
Only tooling (IDEs and plugins) and learning resources still need to catch up the advocated move from `*.jsf` to `*.xhtml`. As per JSF 2.3, the `FacesServlet` will by default be auto-registered on `*.xhtml` too (next to `/faces/*`, `*.faces` and `*.jsf`).
This is back-ported to Mojarra 2.2.11.

---

>[!question] [What is the difference between creating JSF pages with .jsp or .xhtml or .jsf extension](https://stackoverflow.com/questions/7914660/what-is-the-difference-between-creating-jsf-pages-with-jsp-or-xhtml-or-jsf-ex)
>
>I saw some examples creating the JSF pages with `.jsp` extension, other examples creating them with `.xhtml` extension, and other examples choose `.jsf`.
>I just would like to know what the difference is between above extensions when working with JSF pages, and how to choose the appropriate extension.

JSP is an old view technology and widely used in combination with JSF 1.x. Facelets (by some people overgeneralized as [XHTML](https://stackoverflow.com/tags/xhtml/info)) is the successor of JSP and introduced as default view technology of JSF 2.x at end of 2009. When you were seeing JSPs, you were perhaps reading outdated books, tutorials or resources targeted on JSF 1.x. You should generally ignore them when developing with JSF 2.x and head to resources targeted on JSF 2.x, otherwise you may end up in confusion because many things are done differently in JSF 2.x on Facelets.

The `*.jsf` is just one of widely used URL patterns of the `FacesServlet` mapping in `web.xml`. Other ones are `*.faces` and `/faces/*`, but those are from back in the JSF 1.0/1.1 ages. They all do not represent the concrete file extension/path, but just a virtual file extension/path and is to be specified in URLs only like so [http://example.com/contextname/page.jsf](http://example.com/contextname/page.jsf). If you are familiar with basic [Servlets](https://stackoverflow.com/tags/servlets/info), then you should know that the servletcontainer will invoke the servlet when the request URL matches the servlet's URL pattern. So when the request URL matches `*.jsf`, then the `FacesServlet` will be invoked this way. When using JSPs, it would actually execute `page.jsp`. When using Facelets, this would actually compile `page.xhtml`.

Since JSF 2.x you can also use `*.xhtml` as URL pattern. This way you don't need to get confused when specifying URLs. Using `*.xhtml` as URL pattern was not possible in JSF 1.x with Facelets 1.x, because the `FacesServlet` would then run in an infinite loop calling itself everytime. An additional advantage of using `*.xhtml` is that the enduser won't be able to see raw JSF source code whenever the enduser purposefully changes the URL extension in browser address bar from for example `.jsf` to `.xhtml`. It is not possible to use `*.jsp` as URL pattern, because this way the container's builtin `JspServlet`, which is already using that URL pattern, would be overridden and then the `FacesServlet` wouldn't be able to feed on JSPs anymore.

---

- `.jsp` files are generally used for JSF views defined using JavaServer Pages. 
- `.xhtml` files are generally used for JSF views defined using Facelets.

> [!tip] Configuration
> This can be changed via configuration (e.g. see the `javax.faces.DEFAULT_SUFFIX` and `javax.faces.FACELETS_SUFFIX` configuration parameters.)

Other extension mappings (`*.jsf`, `*.faces`) tend to be used for processing requests via the `FacesServlet`. This is a logical mapping to the view which the JSF runtime will handle. How mappings are handled is defined in the `web.xml` (that doesn't have to be done using extensions; the `/faces/*` mapping is often used.

From the spec:

### Servlet Mapping

> All requests to a web application are mapped to a particular servlet based on matching a URL pattern (as defined in the Java Servlet Specification) against the portion of the request URL after the context path that selected this web application.
> ==JSF implementations must support web application that define a `<servlet-mapping>` that maps any valid URL-pattern to the FacesServlet==.
> Prefix or extension mapping may be used.
> When using prefix mapping, the following mapping is recommended, but not required:
```xml
<servlet-mapping>
	<servlet-name> faces-servlet-name </servlet-name>
	<url-pattern>/faces/*</url-pattern>
</servlet-mapping>
```
> When using extension mapping the following mapping is recommended, but not required:
```xml
<servlet-mapping>
	<servlet-name> faces-servlet-name </servlet-name>
	<url-pattern>*.faces</url-pattern>
</servlet-mapping>
```
> In addition to FacesServlet, JSF implementations may support other ways to invoke the JavaServer Faces request processing lifecycle, but applications that rely on these mechanisms will not be portable.

---

### See also:

- [What is the difference between JSF, Servlet and JSP?](https://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp)
- [Why Facelets is preferred over JSP as the view definition language from JSF2.0 onwards?](https://stackoverflow.com/questions/13092161/why-facelets-is-preferred-over-jsp-as-the-view-definition-language-from-jsf2-0-o/)
- [JSF Facelets: Sometimes I see the URL is .jsf and sometimes .xhtml. Why?](https://stackoverflow.com/questions/3008395/jsf-facelets-sometimes-i-see-the-url-is-jsf-and-sometimes-xhtml-why)

---
### See also:

- [Can we use regular expressions in web.xml URL patterns?](https://stackoverflow.com/questions/8570805/can-we-use-regular-expressions-in-web-xml-url-patterns)
- [Set default home page via \<welcome-file\> in JSF project](https://stackoverflow.com/questions/27562813)
- [JSF returns blank/unparsed page with plain/raw XHTML/XML/EL source instead of rendered HTML output](https://stackoverflow.com/questions/3112946)
- [What is the difference between creating JSF pages with .jsp or .xhtml or .jsf extension](https://stackoverflow.com/questions/7914660)
- [Which XHTML files do I need to put in /WEB-INF and which not?](https://stackoverflow.com/questions/9031811)
- [Customize FacesServlet \<url-pattern\> to get rid of .xhtml extension](https://stackoverflow.com/questions/18508329/customize-facesservlet-url-pattern-to-get-rid-of-xhtml-extension/)


---
##### ***References***
- [StackOverflow post_1](https://stackoverflow.com/questions/3008395/sometimes-i-see-jsf-url-is-jsf-sometimes-xhtml-and-sometimes-faces-why)
- [StackOverflow post_2](https://stackoverflow.com/questions/7914660/what-is-the-difference-between-creating-jsf-pages-with-jsp-or-xhtml-or-jsf-ex)
- 