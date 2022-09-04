# Validar sesion

Se crea un archivo jsp que contenga el siguiente código, aquí lo llamamos 'validarSesion.jsp'
>Importante cambiar el atributo que se recibe por el que se crea al iniciar sesión
```JAVA
<%
    response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate");
    response.setHeader("Pragma", "no-cache");
    response.setDateHeader("Expires", 0);

    HttpSession sesion = request.getSession();

    if (sesion.getAttribute("usuario") == null) {
        request.getRequestDispatcher("index.jsp").forward(request, response);
    }
%>
```

# Validar roles
Si tenemos una applicación que maneja distintos roles, lo más común es que cada rol tenga solo acceso a ciertos archivos. Por eso debemos restringir por roles el acceso de estos.

Para este caso, vamos a planter un programa que cuenta con tres roles (admin = 1, empleado = 2, cliente = 3)

>Al momento de iniciar sesión se debe obtener los datos del usuario

Se crea un archivo que redigirá cada rol a su respectivo archivo, para el ejemplo lo llamaremos 'menu.jsp' y tendrá lo siguiente
```JAVA
// Incluimos el archivo que valida que la sesion este activa
<jsp:include page="validarSesion.jsp" />
<%@page import="domain.UsuarioVO"%>
<%
    // Obtenemos la sesión
    HttpSession sesion = request.getSession();

    // Obtenemos los datos que se crearon al iniciar sesión
    UsuarioVO userVo = (UsuarioVO) sesion.getAttribute("usuario");
    // Se obtiene el rol
    String idRol = userVo.getIdRol();

    // Redirigimos según el rol
    if (idRol.equals("1")) {
        response.sendRedirect("admin.jsp");
    } else if (idRol.equals("2")) {
        response.sendRedirect("empleado.jsp");
    } else if (idRol.equals("3")) {
        response.sendRedirect("cliente.jsp");
    } else {
        response.sendRedirect("index.jsp");
    }
%>

```


Se crea un archivo con un nombre descriptivo, en este caso se llama 'validarRolAdmin.jsp'
**En este caso se manejan la información con VO o también conocido como clase de dominio, pero no importa comno se maneje, solo hay que hacer la importación**
```JAVA
<%@page import="domain.UsuarioVO"%>
<%
    // Se obtiene la sesion para acceder a sus datos
    HttpSession sesion = request.getSession();

    // Guardamos la informacion que está almacenada en el atributo de la sesion (el que se creo al iniciar sesion)
    UsuarioVO userVo = (UsuarioVO) sesion.getAttribute("usuario");
    // Guardamos el rol en una variable
    String idRol = userVo.getIdRol();
    // Si un usuario ingresa al archivo y tiene un rol diferente a '1' (admin), lo redireciona a menu.jsp para que allí lo redirecione al archivo que tiene acceso
    if (!idRol.equals("1")) {
        request.getRequestDispatcher("menu.jsp").forward(request, response);
    }
%>
```
Ahora se crea otro archivo para validar uno de los otros dos roles, aquí lo llamamos 'validarRolEmpleado.jsp'
```JAVA
<%@page import="domain.UsuarioVO"%>
<%
    // Se obtiene la sesion para acceder a sus datos
    HttpSession sesion = request.getSession();

    // Guardamos la informacion que está almacenada en el atributo de la sesion (el que se creo al iniciar sesion)
    UsuarioVO userVo = (UsuarioVO) sesion.getAttribute("usuario");
    // Guardamos el rol en una variable
    String idRol = userVo.getIdRol();
    // Si un usuario ingresa al archivo y tiene un rol diferente a '2' (empleado), lo redireciona a menu.jsp para que allí lo redirecione al archivo que tiene acceso
    if (!idRol.equals("2")) {
        request.getRequestDispatcher("menu.jsp").forward(request, response);
    }
%>
```

Por ultimose crea otro archivo para validar el rol faltante, aquí lo llamamos 'validarRolCliente.jsp'
```JAVA
<%@page import="domain.UsuarioVO"%>
<%
    // Se obtiene la sesion para acceder a sus datos
    HttpSession sesion = request.getSession();

    // Guardamos la informacion que está almacenada en el atributo de la sesion (el que se creo al iniciar sesion)
    UsuarioVO userVo = (UsuarioVO) sesion.getAttribute("usuario");
    // Guardamos el rol en una variable
    String idRol = userVo.getIdRol();
    // Si un usuario ingresa al archivo y tiene un rol diferente a '3' (cliente), lo redireciona a menu.jsp para que allí lo redirecione al archivo que tiene acceso
    if (!idRol.equals("3")) {
        request.getRequestDispatcher("menu.jsp").forward(request, response);
    }
%>
```

Si por algún motivo un usuario con un rol, puede acceder a varios archivos de distintos roles solo bastará con agregar el rol en el if. Algo así
```JAVA
<%@page import="domain.UsuarioVO"%>
<%
    if (!idRol.equals("1") && !idRol.equals("2")) {
        request.getRequestDispatcher("menu.jsp").forward(request, response);
    }
%>
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)