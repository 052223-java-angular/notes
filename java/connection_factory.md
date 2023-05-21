# ConnectionFactory Class

```java
package com.revature.yolp.utils;

import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

public class ConnectionFactory {
    private static ConnectionFactory instance;
    private Connection connection;

    private ConnectionFactory() throws ClassNotFoundException, IOException, SQLException {
        Class.forName("org.postgresql.Driver");
        Properties props = getProperties();
        connection = DriverManager.getConnection(
                props.getProperty("url"),
                props.getProperty("username"),
                props.getProperty("password"));
    }

    /* ----------------- Methods ----------------- */

    public static ConnectionFactory getInstance() throws SQLException, ClassNotFoundException, IOException {
        if (instance == null || instance.getConnection().isClosed()) {
            instance = new ConnectionFactory();
        }
        return instance;
    }

    public Connection getConnection() {
        return connection;
    }

    /* ----------------- Helper Methods ----------------- */

    private Properties getProperties() throws IOException {
        Properties props = new Properties();
        try (InputStream input = getClass().getClassLoader().getResourceAsStream("application.properties")) {
            if (input == null) {
                throw new IOException("Unable to find application.properties");
            }
            props.load(input);
        }
        return props;
    }
}
```

This `ConnectionFactory` class resides in the `com.revature.yolp.utils` package and is designed to establish a connection with a database. 

## Static Keyword in Java

In Java, `static` is a keyword that you can use to declare a variable, method, or inner class as belonging to the class itself, rather than to any instance of the class. 

- **Static Variable**: When a variable is declared as `static`, only one copy is created and shared among all instances of the class. This means that even if you create multiple objects of the class, they'll all share the same `static` variable.
- **Static Method**: `Static` methods can be called without creating an instance of the class. They are often used for utility or helper methods that don't rely on any particular state of the object.

**Static Variable**: Think of a static variable as a locker that all students in a school can use. No matter which student (in this case, an instance of a class) uses the locker, the contents of the locker stay the same. If one student puts something in the locker, it will be there for the next student. Similarly, a static variable is shared and can be used by all instances of a class, and any change made to this variable will be seen by all instances.

**Static Method**: A static method is like a tool that anyone can use, like a calculator. You don't need to have a certain calculator (an instance of a class) to do a calculation. Any calculator (the Calculator class itself), no matter who has it or where it is, can add two numbers together. This is like how static methods in Java work. They are part of the class itself and can be used without making an instance of the class. They do the same thing, no matter what the object state is.

## Class Structure

- **Class Variables**
  - `private static ConnectionFactory instance`: Holds the single instance of `ConnectionFactory`.
  - `private Connection connection`: Holds the database connection.

- **Constructor**
  - `private ConnectionFactory()`: The constructor loads the PostgreSQL JDBC driver, reads the database configuration from a properties file, and establishes a connection to the database.

- **Methods**
  - `public static ConnectionFactory getInstance()`: Returns the single instance of `ConnectionFactory`. If no instance exists, or if the existing instance's connection is closed, a new instance is created.
  - `public Connection getConnection()`: Returns the `Connection` object associated with the current `ConnectionFactory` instance.

- **Helper Methods**
  - `private Properties getProperties()`: Reads and returns the properties from the `application.properties` file.

## How It Works

- **Singleton Pattern**
  This class implements the Singleton design pattern to ensure that only a single instance of `ConnectionFactory` exists. This pattern is useful when exactly one object is needed to coordinate actions across the system, like managing database connections.

- **Database Connection**
  The constructor of this class connects to the database by calling `DriverManager.getConnection()`, using the database URL, username, and password read from the `application.properties` file. This connection is then used whenever `getConnection()` is called.

- **Properties File**
  Database connection parameters such as the URL, username, and password are read from a properties file named `application.properties` using the `getProperties()` method. If the file can't be found, an IOException is thrown.

## Importance of Singleton Pattern in ConnectionFactory

The Singleton pattern is particularly useful for the `ConnectionFactory` because it ensures that only one instance of the connection is active at a time. 

In most applications, opening and closing database connections are costly operations in terms of resources and time. By sharing a single connection among different parts of your program, you can minimize these costs and make your program more efficient. Also, having a single connection to a database prevents potential conflicts caused by multiple concurrent connections.

## Benefits of Using a Properties File

Keeping the database connection parameters (URL, username, password) in a separate properties file has several advantages:

- **Security**: You can keep sensitive data (such as the database password) out of your code.
- **Flexibility**: You can change the connection parameters simply by editing the properties file, without needing to modify and recompile your code.
- **Maintainability**: If your application connects to different databases (for example, during testing and production), you can use different properties files for each environment. This makes your code cleaner and easier to maintain.

## Exception Handling

The `IOException` thrown by the `getProperties()` method is an example of exception handling in Java. Exceptions are events that occur during the execution of programs that disrupt the normal flow of instructions. 

In this case, if the properties file `application.properties` cannot be found, an `IOException` will be thrown, indicating that an input or output operation has been failed or interrupted.
