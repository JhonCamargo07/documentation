# Encriptar contraseñas con Bcript

¿Como utlizarlo?
Al projecto, en el archivo 'pom.xml' debe agregar el siguiente fragmento de código (dentro de la etiqueta 'dependencies')

```JAVA
<!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-crypto -->
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-crypto</artifactId>
    <version>5.7.3</version>
</dependency>
```

Seguido a esto, cree un archivo de java y le agrega la siguiente importacion

```JAVA
import org.springframework.security.crypto.bcrypt.BCrypt;
```

Ahora hay que crear los siguientes metodos

```JAVA
/**
    * Este metodo encripta las contraseñas, utilizando spring security
    * @param passwordNotEncript, password sin encriptar
    * @return String, devuelve la contraseña encriptada
    */
public static String encript(String passwordNotEncript){
    return BCrypt.hashpw(passwordNotEncript, BCrypt.gensalt());
}

/**
    * Este metodo verifica si una contraseña sin encriptar es la misma que una contraseña encriptada, utilizando spring security
    * @param passwordNotEncript, password sin encriptar
    * @param passwordEncript, password con encriptacion
    * @return boolean, retorna si una contraseña encriptada es igual a una que no lo esta
    */
public static boolean verifyPassword(String passwordNotEncript, String passwordEncript){
    return BCrypt.checkpw(passwordNotEncript, passwordEncript);
}
```
Y listo eso es todo.

>Ejemplo
```JAVA
String password = "Hola mundó!|\"$%&/()=?¡";
String passwordEncript = encript(password);
System.out.println("passwordEncript = " + passwordEncript);

boolean isPasswordCorrect = verifyPassword("Hola mundó!|\"$%&/()=?¡", passwordEncript);
System.out.println("isPasswordCorrect = " + isPasswordCorrect);
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)