> [!question] [One or multiple servlets per webapp?](https://stackoverflow.com/questions/272118/one-or-multiple-servlets-per-webapp)
> I know, it depends on the webapp. But in the normal case, what do you do: one servlet, that serves different pages (like an standalone-application with changing content) or for every page a single servlet.
> Take for instance a blog. There is the start-page with the most recent blog-entries, an article-view for displaying one blog-entry and an archive. Do you implement this with three different servlets, or one that is dispatching to the functions. At least a good part of the stuff is shared, like http-headers.
> ---
> ==So, what are your experiences, what works best?==

### Servlet per use-case

Usually you will create a servlet per use case.
When you identify an interaction from a user then implement a servlet to control that interaction.

> [!example] Servlets acts like **"Controllers"** for your application
> That is, if you are using plain servlet/JSP to build the site.

If you are using a framework like [Struts](https://struts.apache.org/) you will find that they implement the front controller pattern and use a single servlet that receives all the requests and forwards these requests to action classes that implement the actual logic of the user request.
- **This is much harder to do yourself but its a good practice.**
- This is the reason why so many people use these frameworks.

> [!Success] One per use-case
> The short answer is, *you will create many servlets per webapp since each webapp will expose several use cases*.

---
### Dispatcher Servlet

Most web frameworks use a ==dispatcher servlet== (ex: Spring MVC) that takes care of routing requests to appropriate classes/controllers.

When you start having lots of pages, this approach works best because you have a more user friendly way (in regard to `web.xml`) of declaring/managing a class that handles http requests and its url.

###### Example (spring mvc again):
```java
@Controller
public class MyController {
 @RequestMapping("/viewPosts")
 public void doViewPosts(HttpRequest r, HttpResponse res) {
  //...
 }
}
```

> [!success] One Dispatcher Servlet
> Having a dispatcher servlet keeps your code flow centralized.
> More user friendly way of declaring Controllers (which would be One per Servlet/Functionality)

---

### No-Framework solution

In my latest projects, I have implemented a single servlet that delegates to several servlet-like objects which are instantiated in a dependency injection fashion.

For instance, I have something like this in my servlet (pseudo-code):
```java
for(Handler handler : handlers) {
    if(handler.handle(request, response)) {
         return;
    }
}
```

where Handler is an interface with a **boolean** `handle(request, response)` method.
I obtain my handlers from a container (be it Spring or something even more lightweight).

The reason for this is that I really like dependency injection, and it is difficult to achieve it in Servlets; and I really don't feel much at home with most frameworks that provide web-component dependency injection.
I like the simplicity of servlets.

Were not for this, I would go with multiple servlets, although there's a trade-off; either you have an enormous `web.xml` with lots (and lots) of servlet mappings or you have a very complex servlet (unless you use something like my *dependency-injection* approach).

---
##### ***References***
- [StackOverflow post](https://stackoverflow.com/questions/272118/one-or-multiple-servlets-per-webapp)