# Borrar el cache

En java
```JAVA
<%
    response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate");
    response.setHeader("Pragma", "no-cache");
    response.setDateHeader("Expires", 0);
%>
```

En html
```JAVA
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate">
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Expires" content="0">
```

>Ejemplo en un jsp

En este caso, el nombre del archivo es 'cache.jsp'
```jsp
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
        <%
            response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate");
            response.setHeader("Pragma", "no-cache");
            response.setDateHeader("Expires", 0);
        %>
    </body>
</html>
```

Se debe incorporar en el jsp así
```JAVA
<%@include file="cache.jsp" %>
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)