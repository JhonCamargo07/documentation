# Validaciones

**Algunos metodos para validar**

Validar email

```Java
/**
 * Este metodo es para validar que el correo que ingresa un usuario tenga el
 * formato correcto
 *
 * @param email, correo que ingresa el usuario
 * @return boolean, retorna si el correo esta bien o no
 */
public static boolean esEmailCorrecto(String email) {
    // Patrón para validar el email
    Pattern pattern = Pattern
            .compile("^[_A-Za-z0-9-\\+]+(\\.[_A-Za-z0-9-]+)*@"
                    + "[A-Za-z0-9-]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$");

    Matcher mather = pattern.matcher(email);

    if (mather.find() == true) {
        return true;
    } else {
        return false;
    }
}

```

Validar passwords
```Java
public static final int CANTIDAD_MINIMA_PASSWORD = 10;
/**
 * Este metodo es para saber si una clave tiene los caracteres minimos
 *
 * @param pass, clave que envia el usuario
 * @return boolean, Retorna si la clave es correcta o no
 */
public static boolean esPasswordCorrecto(String pass) {
    if (!pass.equals("")) {
        if (pass.length() < Validaciones.CANTIDAD_MINIMA_PASSWORD) {
            return true;
        }
    }
    return false;
}
```

Validar string
```Java
/**
     * Este metodo es para saber si un String no es nulo
     * @param string, Cadena proporcionada por el usuario
     * @return boolean, retorna si la cadena es nula o no
     */
    public static boolean esStringNulo(String string) {
        return string.equals("");
    }
```

```Java

```
