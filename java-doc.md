# JavaDoc

## Tipos de etiquetas

**Las etiquetas empiezan con @**
Ejemplo

```JAVA
/**
* @author Jhon Camargo
* @version 1.0.0 08/2022
* @since 1.0.0
*/
```

1. autor: Quien hizo la clase
2. version: Version de la clase
3. param: Parametros de un metodo
4. Return: El valor que retorna un metodo
5. Thorws: Excepciones
6. See: Lanzar a otros metodos o clases (Clase a la que depende)
7. deprecated: Metodos o clases que van a desaparecer en el futuro
8. Since: Dede que version estara disponible la clase

# Ejemplos

**Nota**

> Los metodos y las clases deben iniciar con una descripcion
> Solo podemos añadir etiquetas html p y a

Ejemplo para una clase

```JAVA
/**
* Esta clase se utiliza para definir los parametros que se van a necesitar en
* el transcurso del proyecto <b>(Clase de dominio)</b>
*
* @author <a href="http://jhoncamargo.000webhostapp.com">Jhon Camargo</a>
* @version 1.0.0 08/2022
* @since 1.0.0
*/
```

Ejemplo para un metodo

```JAVA
/**
* Este metodo se encarga de insertar usuarios a la base de datos
*
* @param usuarioVo Es el objeto que conserva todos los datos del usuario a
* registrar
* @return boolean Es el valor de la operacion, si se hizo o no la insersion
* en la base de datos
* @throws SQLException, Esta excepcion se lanza cuando ocurre algun error
* al hacer la insercion en la base de datos
*/
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)