# Pagina para redirigir a otra pagina

Esta pagina tiene la funcionalidad de redirecionar a otra pagina que se le indica, esto para reducir las probabilidades de que los archivos js que se llamen no se incorporen correctamente (Error 500).

En ocaciones, cuendo programamos en java y queremos redirecionar a una vista desde un controlador o servlet y mostrar un mensaje con una alerta, los archivos js que se deberían incorporar no lo hacen de manera correcta y se genera un error 500. Para solucionar este error se plantea la siguiente solución:

En el servlet se crea un atributo que se llame redirigir y como valor le asignamos la pagina a la que queremos que se redirija
```JAVA
String redirigirA = "menu-inicio.jsp";
request.setAttribute("redirigir", redirigirA);
request.getRequestDispatcher("redirigir.jsp").forward(request, response);
```

Continuando con el codigo anterior, ahora debemos crear un archivo jsp llamado 'redirigir.jsp' que contenga el siguiente código
```JAVA
<%
    if(request.getAttribute("redirigir") != null){
        String redirigirA = (String) request.getAttribute("redirigir");
        request.getRequestDispatcher(redirigirA).forward(request, response);
    }
%>
```
Con esta solución se podría dejar a un lado este error.

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)