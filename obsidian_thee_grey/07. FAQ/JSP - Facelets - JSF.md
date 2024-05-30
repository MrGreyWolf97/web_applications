> [!question]
> I can't seem to get a clear answer as to the concrete difference between ==JSF== vs. so-called ==Facelets==
> 
> Also, I understand that either JSF or JSP can be used to create dynamic web pages, but two seemingly-conflicting details are confusing me. I've heard both of the following:
>
> 1. That JSF is a replacement for JSP; and
> 2. JSF and JSP form different parts of the _View_ in Java's web-tier MVC paradigm
> 
> So which is it?
> Logic dictates it almost certainly can't be both!


- JSF is a standardized ***==Java framework==*** for web UIs based on an MVC pattern, built on top of
- JSPs is a (much older) ***==standard==*** for generating web pages from templates - these _can_ be used as the View in a JSF application, but also separately from JSF.
- Facelets are an alternative view technology based on pure XML templates (no scriptlets) which was introduced with Version 2 of the JSF standard.
  They can only be used in a JSF application.

In the light of that, let's take a look at your conflicting statements:

> [!success] That JSF is a replacement for JSP
> Not quite true, since JSF can use JSPs for its view (and had to, prior to JSF 2).
> However, JSF apps using Facelets can be seen as a replacement for JSP-based technologies.

> [!error] JSF and JSP form different parts of the View in Java's web-tier MVC paradigm
> Completely wrong - JSF covers the entire MVC pattern, though it can overlap with EJBs, since both are based on annotations that can be mixed in the same class.


---
## JSP vs Facelets

**==Java Server Pages (JSP)==** is java technology that enables Web developers and designers to rapidly develop and easily maintain, information-rich, dynamic Web pages that leverage existing business systems. 
JSP technology separates the user interface from content generation, enabling designers to change the overall page layout without altering the underlying dynamic content.  
  
**==Facelets==** is the first non-JSP page declaration language designed for JSF (Java Server Faces) which provided a simpler and more powerful programming model to JSF developers as compared to JSP. It resolves different issues that occur in JSP for web application development.  
  
In the below table, a difference between Facelets and JSP is shown by comparing different features of JSP and Facelets.  
  

|                            |                                                                                                                                             |                                                                                                                                               |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Feature Name**           | **JSP**                                                                                                                                     | **Facelets**                                                                                                                                  |
| Pages are compile          | A Servlet that gets executed each time the page renders.<br>The UI Component hierarchy is built by the presence of custom tags in the page. | An abstract syntax tree that, when executed, builds a UI Component hierarchy                                                                  |
| Handling of tag attributes | All tag attributes must be declared in<br>a TLD file.                                                                                       | Tag attributes are completely dynamic and automatically map to properties, attributes, and Value Expressions on<br><br>UI Component instances |
| Page template              | Not supported directly.<br>For templating must go outside of core JSP                                                                       | Page templating is a core feature of Facelets                                                                                                 |
| Performance                | Due to the common implementation technique of compiling a JSP page to a Servlet, performance can be slow                                    | Facelets is simpler and faster than JSP                                                                                                       |
| EL Expressions             | Expressions in template text cause unexpected behavior when used in JSP                                                                     | Expressions in template text operate as expected.                                                                                             |
| JCP Standard               | Yes, the specification is separate from the implementation for JSP                                                                          | No, the specification is defined by and is one with the implementation.                                                                       |


---
##### ***Resources***
- [Difference between JSP and Facelets](https://javawebaction.blogspot.com/2012/05/difference-between-jsp-and-facelets.html)