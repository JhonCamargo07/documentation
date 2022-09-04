# Conectarse a una bd con JDCB y pool de conexiones

Se debe crear la clase Conexion, luego dentro de ella se coloca lo siguiente.
>Se debe editar la constante 'NAME_DB', asignandole como valor el nombre de la base de datos
```JAVA
import java.sql.*;
import java.util.logging.*;
import javax.sql.DataSource;
import org.apache.commons.dbcp2.BasicDataSource;
```

>Si se desea, de puede agrandar o reducir el pool de conexiones
```JAVA
private static final String NAME_DB = "name-bd";
private static final String JDBC_URL = "jdbc:mysql://localhost:3306/" + NAME_DB + "?useSSL=false&useTimezone=true&serverTimezone=UTC&allowPublicKeyRetrieval=true";
private static final String JDBC_USER = "root";
private static final String JDBC_PASS = "";

private static BasicDataSource dataSource;

public static DataSource getDataSource() {
    if (dataSource == null) {
        dataSource = new BasicDataSource();
        dataSource.setUrl(JDBC_URL);
        dataSource.setUsername(JDBC_USER);
        dataSource.setPassword(JDBC_PASS);
        dataSource.setInitialSize(25);
    }
    return dataSource;
}

public static Connection getConnection() throws SQLException {
    return getDataSource().getConnection();
}

public static void close(ResultSet rs) {
    try {
        rs.close();
    } catch (SQLException ex) {
        System.out.println("Error al cerrar el ResultSet");
        Logger.getLogger(Conexion.class.getName()).log(Level.SEVERE, null, ex);
    }
}

public static void close(PreparedStatement stmt) {
    try {
        stmt.close();
    } catch (SQLException ex) {
        System.out.println("Error al cerrar el PreparedStatement");
        Logger.getLogger(Conexion.class.getName()).log(Level.SEVERE, null, ex);
    }
}

public static void close(Connection conn) {
    try {
        conn.close();
    } catch (SQLException ex) {
        System.out.println("Error al cerrar la conexion");
        Logger.getLogger(Conexion.class.getName()).log(Level.SEVERE, null, ex);
    }
}
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)