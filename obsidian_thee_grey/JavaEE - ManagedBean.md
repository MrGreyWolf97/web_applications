

>[!warning]
>To be moved to Notion documentation


---



The presence of this annotation on a class ==automatically registers the class with the runtime as a managed bean class==.
Classes must be scanned for the presence of this annotation at application startup, before any requests have been serviced.

#### Attribute: *name*
The value of the [name](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html "command:java.open.file?%5B%22jdt%253A%252F%252Fcontents%252Fjsf-api-2.1.7.jar%252Fjavax.faces.bean%252FManagedBean.class%253F%253Dlocal%252F%25255C%252Fhome%25255C%252Fmr_grey_wolf%25255C%252F.m2%25255C%252Frepository%25255C%252Fcom%25255C%252Fsun%25255C%252Ffaces%25255C%252Fjsf-api%25255C%252F2.1.7%25255C%252Fjsf-api-2.1.7.jar%253D%252Fmaven.pomderived%253D%252Ftrue%253D%252F%253D%252Fjavadoc_location%253D%252Fjar%253Afile%253A%25255C%252Fhome%25255C%252Fmr_grey_wolf%25255C%252F.m2%25255C%252Frepository%25255C%252Fcom%25255C%252Fsun%25255C%252Ffaces%25255C%252Fjsf-api%25255C%252F2.1.7%25255C%252Fjsf-api-2.1.7-javadoc.jar%25255C!%25255C%252F%253D%252F%253D%252Fmaven.groupId%253D%252Fcom.sun.faces%253D%252F%253D%252Fmaven.artifactId%253D%252Fjsf-api%253D%252F%253D%252Fmaven.version%253D%252F2.1.7%253D%252F%253D%252Fmaven.scope%253D%252Fcompile%253D%252F%253D%252Fmaven.pomderived%253D%252Ftrue%253D%252F%25253Cjavax.faces.bean%252528ManagedBean.class%2523111%22%5D") attribute is taken to be the _managed-bean-name_. If the value of the _name_ attribute is unspecified or is the empty `String`, the _managed-bean-name_ is derived from taking the unqualified class name portion of the fully qualified class name and converting the first character to lower case. For example, if the `ManagedBean` annotation is on a class with the fully qualified class name `com.foo.Bean`, and there is no _name_ attribute on the annotation, the _managed-bean-name_ is taken to be `bean`. The fully qualified class name of the class to which this annotation is attached is taken to be the _managed-bean-class_.

#### Scope
The scope of the managed bean is declared using one of NoneScoped, RequestScoped, ViewScoped, SessionScoped, ApplicationScoped, or CustomScoped) annotations.
If the scope annotations are omitted, the bean must be handled as if the **RequestScoped** annotation is present.
-> ==RequestScope is the default==


If the value of the [eager](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html "command:java.open.file?%5B%22jdt%253A%252F%252Fcontents%252Fjsf-api-2.1.7.jar%252Fjavax.faces.bean%252FManagedBean.class%253F%253Dlocal%252F%25255C%252Fhome%25255C%252Fmr_grey_wolf%25255C%252F.m2%25255C%252Frepository%25255C%252Fcom%25255C%252Fsun%25255C%252Ffaces%25255C%252Fjsf-api%25255C%252F2.1.7%25255C%252Fjsf-api-2.1.7.jar%253D%252Fmaven.pomderived%253D%252Ftrue%253D%252F%253D%252Fjavadoc_location%253D%252Fjar%253Afile%253A%25255C%252Fhome%25255C%252Fmr_grey_wolf%25255C%252F.m2%25255C%252Frepository%25255C%252Fcom%25255C%252Fsun%25255C%252Ffaces%25255C%252Fjsf-api%25255C%252F2.1.7%25255C%252Fjsf-api-2.1.7-javadoc.jar%25255C!%25255C%252F%253D%252F%253D%252Fmaven.groupId%253D%252Fcom.sun.faces%253D%252F%253D%252Fmaven.artifactId%253D%252Fjsf-api%253D%252F%253D%252Fmaven.version%253D%252F2.1.7%253D%252F%253D%252Fmaven.scope%253D%252Fcompile%253D%252F%253D%252Fmaven.pomderived%253D%252Ftrue%253D%252F%25253Cjavax.faces.bean%252528ManagedBean.class%2523118%22%5D") attribute is `true`, and the `managed-bean-scope` value is "application", the runtime must instantiate this class when the application starts.
This instantiation and storing of the instance must happen before any requests are serviced. If _eager_ is unspecified or `false`, or the `managed-bean-scope` is something other than "application", the default "lazy" instantiation and scoped storage of the managed bean happens.

When the runtime processes this annotation, if a managed bean exists whose name is equal to the derived _managed-bean-name_, a `FacesException` must be thrown and the application must not be placed in service.

A class tagged with this annotation must have a public zero-argument constructor. If such a constructor is not defined on the class, a `FacesException` must be thrown and the application must not be placed in service.
