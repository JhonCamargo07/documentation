# Enviar correos con JavaMail

Se crea una clase en java y se añadenlas siguientes importaciones
```JAVA
import java.util.*;
import javax.mail.*;
import javax.mail.internet.*;
```

Luego dentro de la clase, se coloca el siguiente fragmento de código
```JAVA
/**
 * Este metodo se encarga de enviar correos
 * @param server, el servidor que usará para ser enviado
 * @param port, el puerto que se utilizará para enviar el correo
 * @param mail,la direccion de correo con la que se enviara al destinatario
 * @param password, contraseña de la persona que va a enviar el correo (contrtaseña del parametro anterior)
 * @param address, email al que se enviara el correo (destinatario)
 * @param affair, asunto con el que se enviara el correo
 * @param message, mensaje con el que se enviara el correo
 * @throws AddressException, en caso de que ocurra algun error con los correos
 * @throws MessagingException, en caso de que ocurra un error al enviar el correo
 */
public static void sendMail(String server, String port, final String mail, final String password, String address, String affair, String message) throws AddressException, MessagingException {
    // Configuracion del SMTP
    Properties property = new Properties();

    property.put("mail.smtp.host", server);
    property.put("mail.smtp.port", port);
    property.put("mail.smtp.auth", "true"); // Autenticar el inicio de sesión
    property.put("mail.smtp.starttls.enable", "true"); // Asegurar que el tls esté activo
    property.put("mail.smtp.starttls.required", true);
    property.put("mail.smtp.ssl.protocols", "TLSv1.2");
    property.put("mail.smtp.ssl.trust","smtp.gmail.com");

    Authenticator autenticar = new Authenticator() {
        public PasswordAuthentication getAuthentication() {
            return new PasswordAuthentication(mail, password);
        }
    };

    Session sesion = Session.getInstance(property, autenticar);

    Message msg = new MimeMessage(sesion);
    msg.setFrom(new InternetAddress(mail));

    InternetAddress[] addresses = {new InternetAddress(address)};
    msg.setRecipients(Message.RecipientType.TO, addresses);
    msg.setSubject(affair);
    msg.setSentDate(new Date());
    msg.setText(message);

    Transport.send(msg, mail, password);

}
```

Luego debemos pasarle los parametros con los que se enviará el correo, esto lo hacemos en la carpeta 'WEB-INF' en el archivo 'web.xml' (src\main\webapp\WEB-INF\web.xml)
```XML
<context-param>
    <param-name>server</param-name>
    <param-value>smtp.gmail.com</param-value>
</context-param>
<context-param>
    <param-name>port</param-name>
    <param-value>587</param-value>
</context-param>
<context-param>
    <param-name>user</param-name>
    <param-value>practicasjhoncamargo@gmail.com</param-value>
</context-param>
<context-param>
    <param-name>password</param-name>
    <param-value>byvqdsvvbiwlkllz</param-value>
</context-param>
```


Para poder utilizar el método que envia los correos se debe crear un servlet y colocar lo siguiente
```JAVA
private String server, port, mail, password;

public void init() {
    ServletContext contex = getServletContext();
    server = contex.getInitParameter("server");
    port = contex.getInitParameter("port");
    mail = contex.getInitParameter("user");
    password = contex.getInitParameter("password");
}
```

>Ejemplo
```JAVA
String asunto = "";
String mensaje = "";
String emailUser = "email@mail.com";

asunto = "Registro exitoso";
mensaje = "¡Bienvenido!\nAcabas de registrarte en nuestro sitio web, es un placer que pertenezcas a esta gran familia.";
try {
    SendEmail.sendMail(server, port, mail, password, emailUser, asunto, mensaje);
} catch (MessagingException ex) {
    System.out.println("Ocurrio un error al enviar el correo");
    Logger.getLogger(Controller.class.getName()).log(Level.SEVERE, null, ex);
}
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)