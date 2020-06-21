---
layout: post
title:  "JDBC Connectivity"
date:   2020-06-20 16:38:54 +0530
categories: Tech

---
## Steps to interact with database using JDBC

1. Create Driver Class
2. Create Connection
3. Create Statement
4. Execute Query
5. Close connection

```
Class.forName("oracle.jdbc.driver.OracleDriver");

Connection con=DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe","neo4j","password");

Statement stmt=con.createStatement();
```

```
ResultSet rs=stmt.executeQuery("select * from emp");  
  
while(rs.next()){  
System.out.println(rs.getInt(1)+" "+rs.getString(2));  
}  
```

`con.close();`