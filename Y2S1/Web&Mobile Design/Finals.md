# Chapter 1
**Suggest an appropriate software stack** (for hosting ASB.NET web application)
- Operating System: Windows Server
- Web Server: Internet Information Services (IIS)
- Database Server: SQL server
- Programming Runtime: .NET 10 (cross-platform)
### 3 Core Component of MVC Web Architecture

| Component  | Model                             | View                                | Controller                           |
| ---------- | --------------------------------- | ----------------------------------- | ------------------------------------ |
| Layer      | Data                              | Presentation                        | Application                          |
| Definition | Represent data of the application | Template files the application user | Handle income request                |
| Eg         | Database, entity classes          | HTML, CSS                           | C# controller classes, action method |
**Advantage of MVC web architecture**
- seperate of concerns
	- each MVC components focuses of specify task (module)
- task distribution
	- making it easier to distribute task among developers, database administrator and designer
		- developer focus on controller
		- database administrator focus on models
		- designer focus on views
- Reusable
	- MVC application is modular

**Advantage of using ASB.NET platform for develop web application**
- Existing software environment
	- many companies may already use Windows-based software
- Customer support
	- Windows-based software are usually paid
- Expendability and scalability
	- Companies and businesses will grow and expend

### URL Routing
Why URL Routing is necessary for ASP .NET MVC web applications
- URL routing engine maps incoming request (URLs) against the routing rules
URL Mapping Analysis
- https://www.website.com/Product/Update/P001?quantity=123
	- Controller: Product
	- Action Method: Update
	- ID Parameter: P001
	- Query String Parameter: quantity
		- value is 123
```C#
public class ProductController :
{
	public IActionResult Update (string id, int quantity)
	{
	}
}
```
---
# Chapter 2
**Advantage of using reusable layout in ASP.NET MVC web applications**
- Provide users with consistent experience as they navigate from page to page
- Layout reduce duplicate code in views

| Tag helpers                                                  | HTML helpers                                                     |     |
| ------------------------------------------------------------ | ---------------------------------------------------------------- | --- |
| Written as HTML elements with custom non-standard attribute  | Written as C# methods. Work  like function calls with parameters |     |
| Codes are clean, concise and easier to understand            | Codes are usually more verbose and slightly complicated          |     |
| Codes are more readable as they resemble typical HTML syntax | Codes are less readable as HTML and C# codes are mixed together  |     |

---
# Chapter 3
**Define unobtrusive JavaScript**
- Seperate of JavaScript behavior from HTML markup
- Avoid the use of inline JavaScript for event handling

**Discuss the advantage of writing unobtrusive JavaScript**
- Modularity
	- Making JS module plug-able to reusable
- Task distribution
	- Web designer can work on HTML and CSS without worrying how to program JS code
- Maintainability
	- making the code easier to read (less emssy)

**Discuss AJAX programming technique and its advantages**
- AJAX is Asynchronous JavaScript and XML
- Handle HTTP request and response using JavaScript running in the background
- Allow form submission and content update without the need of reloading whole page
- Advantage
	- Improve responsiveness and user experience

---
# Chapter 4
**Object-relational mapping (ORM)**
- a process of converting data in a relational database into object-oriented representations

| Relational   | Object      |
| ------------ | ----------- |
| Table        | Class       |
| Column       | Property    |
| Relationship | Association |
| Record (Row) | Object      |

| Database-First                                                        | Code-First                                                         |
| --------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Develop database first. Then generate entity classes  automatically   | Develop entity classes first. Then generate database automatically |
| Popular for database administrators who focus on database development | Popular for programmers who focus on application development       |
| Suitable when working with existing database                          | Suitable when the database has not been created                    |

---
# Chapter 5

### Request method

| GET                                         | POST                                                 |
| ------------------------------------------- | ---------------------------------------------------- |
| To retrieve resource from web server        | To create, modify or remove resource from web server |
| For action that does not alter server state | For action that alters server state                  |
| No side effect                              | Has side effect                                      |
| SELECT                                      | INSERT, UPDATE, DELETE                               |
**Identify**
- Select a student record
	- GET, because it does not alter server state or data
- Insert a student record
	- POST, because it alter server state or data

### Advantage & disadvantage of using ExecuteUpdate() and ExecuteDelete()

| Advantage                                                                              | Disadvantage                                                |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Allow update or delete one or multiple records without pre-select the targeted records | The syntax is more SQL-oriented rather than objext-oriented |
| The underlying SQL query is generated and send directly to the database for execution  | The syntax may be less readable for UPDATE operation        |
| Less memory usage                                                                      |                                                             |

---
# Chapter 6

### Difference side input validation

| Client-Side                                    | Server-Side                                          |
| ---------------------------------------------- | ---------------------------------------------------- |
| Program using JS, Run at browser (locally)     | Program using C#, Run at the server (remotely)       |
| incapable to perform complex validation logics | involve roundtrip, less responsive                   |
| Insecure, client can easily turn off JS        | Secure, server-side input validations always running |

| Strongly-typed models                                  | ViewBag Properties                                              |
| ------------------------------------------------------ | --------------------------------------------------------------- |
| A view can only accept one model                       | Capable to pass multiple data to view                           |
| Support auto code completion and design-time debugging | Does not support auto code completion and design-time debugging |
| used to hold main (primary) data of the page           | used to hold sub (secondary) data of the page                   |

---
# Chapter 7
**Image processing technique**
- Image Cropping
	- Cut or drop the excessive portions of the image
- Image Resizing
	- Reduce the dimension of the image
- Image Type Conversion
	- Convert image of different types to a single consistent type
	- for example: (BMP, PNG convert to JPG)
---
# Chapter 8

| Authentication                                                                                           | Authorization                                                                          |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Process of ascertaining the identity of a user, ensure if the user is really the one who he claims to be | process of allow or deny a user from accessing protected pages, functions or resources |
| Logging in with a password or OTP                                                                        | An admin editing a post while a guest can only view it                                 |
```C#
[Authorize]
public IActionResult Page1() {...}

[Authorize(Roles = 'Admin')]
public IActionResult Page2() {...}

[Authorize(Roles = "Admin, Member")]
public IActionResult Page3() {...}
```
**Effect**
- line 1
	- Require the user to be authenticated, any logged-in user can access
- line 4
	- Only users with the **Admin** role can access, others will be denied
- line 7
	- Only users with **Admin** or **Member** roles can access. User with neither role are denied

**Web optimization technique**
- Bundling
	- Combine multiple smaller JS/CSS files together as a single larger file
	- Making multiple HTTP request can increase web app loading time
- Minification
	- Reduce JS/CSS file size by removing unnecessary characters
	- Also rename identifiers to shorter names