---
layout: post
title: "Maven, JDBC, and Servlets"
tags:
 -
---
# Advanced Java, J2EE : Day 2

# Day 2

1. `Maven Project`
2. `JDBC` with `MYSQL application`
3. Convert the application to web application using `servlet`, `JSP`, `Session Handling`

### Maven

→ Dependency Management, including transitive dependency

→ Consistency across all team members(No need to manually download from different websites. Maven will do that for us)

→ Standard structure for Application for different IDE

→ Automation for compile, test, build, and bundle via goals

Java provides interfaces and database vendors provide the implementation class

Steps to connect to MySQL

1. Load Vendor class to JVM(Class.forName('oracle.jdbc.OracleDriver'))
2. Establish Database Connection

    `java.sql.Connection con = DriverManager.getConnection(URL, UserName, Password)`

3. Send SQL statements(`statement`, `Callable Statement,` `Prepared statement)`
4. ResultSet(Cursor to iterate  data)
5. Close the connection → Finally Block

### Web Application Development

1. Static Content
2. Servlet → Server Side Java Code
3. JSP → Static + Dynamic
4. Filter → Interceptor design pattern for security, logging
5. Listener → Activity based on events

Engine/Container/helper_application : Tomcat, Jetty, JRocket.

Servlet Containers have thread pools

### Servlets

threadLocal APIs and threadpools

ArrayBlocking Queue

---

Servlets!

`web.xml` → Deployment Descriptor

```java
<servlet>
	<servlet-name>One</servlet-name>
	<servlet-class><pkg.RegisterServlet/servlet-clas>
</servlet>

<servlet-mapping>
	<servlet-name>One</servlet-name>
	<url-pattern>/register</url-pattern>
</servlet-mapping>
```

From `Servlet API 2.5` onwards we use Annotation

`res.sendRedirect` is used for client Side Redirection with 302 header

```java
package com.cisco.prj.web;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.cisco.prj.dao.DaoException;
import com.cisco.prj.dao.ProductDao;
import com.cisco.prj.dao.ProductDaoJdbcImpl;
import com.cisco.prj.entity.Product;
 
@WebServlet("/products")
public class ProductServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
 
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html"); // MIME type
		PrintWriter out = response.getWriter(); // opens character stream to browser
		//ServletOutputStream out = response.getOutputStream(); // byte stream
		out.print("<html>");
		out.print("<body>");
		out.print("<h1>Products</h1>");
		out.print("<table border=\"1\">");
		out.print("<tr><th>Name</th><th>Price</th><th>Quantity</th></tr>");
		ProductDao productDao = new ProductDaoJdbcImpl();
		
		try {
			List<Product> list = productDao.getProducts();
			for(Product p : list) {
				out.print("<tr>");
					out.print("<td>" + p.getName() + "</td>");
					out.print("<td>" + p.getPrice() + "</td>");
					out.print("<td>" + p.getQuantity() + "</td>");
				out.print("</tr>");
			}
		} catch (DaoException e) {
			e.printStackTrace();
			response.sendRedirect("error.jsp?msg=" + e.getMessage());
		}
		
		out.print("</table></body></html>");
		
		
		
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		ProductDao productDao = new ProductDaoJdbcImpl();
		Product p = new Product();
		p.setName(request.getParameter("name"));
		p.setPrice(Double.parseDouble(request.getParameter("price")));
		p.setQuantity(Integer.parseInt(request.getParameter("quantity")));
		
		try {
			productDao.addProduct(p);
			response.sendRedirect("index.html");
		} catch (DaoException e) {
			response.sendRedirect("error.jsp?msg=" + e.getMessage());
		}
	}

}
```

`ResourceBundle res = ResourceBundle.getBundle("config");`  Used to access Resource properties File

`Class.forName(DRIVER);`

### JSP Pages  and JSTL

Internally, It is `servlet` too.

Can have static and dynamic content

Translation Phase → Change JSP to Servlet [JSPc : JSP → Java]

Request Processing phase

${[p.id](http://p.id/)} is same as p.getId() in JSTL

Servlet, JSP, Client Side Redirection and Server Side Redirection

Session Tracking ==> Http Protocol is a stateless protocol [ request and response objects are short-lived; created and destroyed for every client request] 
Session Tracking is the ability to server side code to keep track of conversational state of client
==> HttpSession API

### Filter → Protected resource

→ Based on Interceptor pattern. Usecase could be to check if user has logged In

Req/Res → once per HTTP

Session → Once per user, destroyed on logout

Servlet Context → Once per application, shared by all users of the application ==> Chatting Application ==> Bid application

Used `@WebFilter` annotation and Implements FilterClass.  Also implements `doFilter(ServletRequest request, ServletResponse response,FilterChain chain)` method

chain.doFilter(request, response);  Passed the request and response down the `FilterChain chain`

```java
package com.cisco.prj.web;

import java.io.IOException;

import javax.servlet.DispatcherType;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

 
@WebFilter(urlPatterns = "*.jsp",dispatcherTypes = {
		DispatcherType.REQUEST, 
		DispatcherType.FORWARD
})
public class SecuirtyFilter implements Filter {
 
    public SecuirtyFilter() {
    }

	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		HttpServletRequest req = (HttpServletRequest) request;
		HttpServletResponse res = (HttpServletResponse) response;
		HttpSession ses = req.getSession(false);
		String uri = req.getRequestURI();
		System.out.println(uri);
		if( (ses != null && ses.getAttribute("email") != null) || uri.endsWith("login.jsp")) {
			chain.doFilter(request, response);
		} else {
			res.sendRedirect("login.jsp");
		}
		
	}

	public void init(FilterConfig fConfig) throws ServletException {
	}

}
```

---

### Listeners

→ Gets invoked based on events happening within servlet engine

- **ServletContxextListener**

    ContextInitialized(), contextDestroyed()

- **HttpSessionListener**

    SessionCreated(), SessionDestroyed()

- **HttpSessionAttributeListener**

```java
package com.cisco.prj.web;

import java.util.HashMap;

import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;
import javax.servlet.annotation.WebListener;

@WebListener
public class ContextLoaderListener implements ServletContextListener {

    public ContextLoaderListener() {
    }

    public void contextDestroyed(ServletContextEvent sce)  { 
    }

    public void contextInitialized(ServletContextEvent sce)  { 
    	System.out.println("Context created!!!");
    	// initialize users and place them in ServletContext
    	HashMap<String, String> users = new HashMap<String, String>();
    	users.put("gavin@apache.com", "secret123");
    	users.put("tim@msn.com", "secret123");
    	users.put("roger@cisco.com", "secret123");
    	
    	sce.getServletContext().setAttribute("users", users);
    }
	
}
```