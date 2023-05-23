# Log4j Configuration Guide

Created by: Jean Duong
Created time: May 22, 2023 9:05 PM
Last edited by: Jean Duong
Last edited time: May 22, 2023 9:19 PM
Tags: Misc

Log4j is a reliable, fast, and flexible logging framework (APIs) written in Java. To configure Log4j2, we typically use an XML, JSON, or YAML file. In this guide, we'll use XML.

## **Directory Structure**

The Log4j2 configuration file (**`log4j2.xml`**) should be placed in the **`src/main/resources`** folder of your project. Log4j2 will automatically look for its configuration file in the classpath.

## **Basic Configuration**

A basic configuration XML file might look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
    <Appenders>
        <File name="File" fileName="src/main/resources/app.log" append="true">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </File>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="File"/>
        </Root>
    </Loggers>
</Configuration>
```

## **Breaking Down the Configuration**

- **`Configuration`**: This is the root element of the configuration file. The **`status`** attribute controls the internal logging of Log4j2. Set to **`WARN`**, this means only warnings or errors encountered during configuration will be output to the console.
- **`Appenders`**: This section is where you define your **`Appenders`**. **`Appenders`** are responsible for delivering LogEvents to their destination.
- **`File`**: The **`File`** appender is used to write log events to a specified file. In this case, **`src/main/resources/app.log`**. The **`append`** attribute is set to **`true`**, meaning that new log events will be appended to the end of the file, rather than overwriting it.
- **`PatternLayout`**: This element inside the **`File`** appender defines the format in which log messages will be written to the file. The pattern **`"%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"`** specifies that each log message will include the date, thread, level, logger, and message, in that order.
- **`Loggers`**: This is where you define the loggers in your application. A logger is named and its name is case-sensitive.
- **`Root`**: The **`Root`** logger sits at the top of the logger hierarchy. It is a special logger that exists in all logging frameworks. In this configuration, it is associated with the **`File`** appender and set to the **`info`** level, meaning it will log all events of level **`info`** and above.

## **Logging Levels**

Log4j has several standard levels of logging. Here are the most common, in order of lowest to highest priority:

- **`TRACE`**: This is the lowest level and is meant to provide very detailed output about the system's behavior. This is typically only useful during development and debugging.
- **`DEBUG`**: This provides more detailed information about the system's state than **`INFO`**, but less detail than **`TRACE`**. It is useful for debugging problems that are not easily reproducible.
- **`INFO`**: This level provides informational messages that highlight the progress of the application. These messages should not occur frequently during normal system use.
- **`WARN`**: Indicates that there might be a problem but it's not severe enough to disrupt the program's execution. These messages are typically logged when there are potential issues that should be noted, but the program can still function.
- **`ERROR`**: Denotes that an error occurred that might prevent the system from functioning properly. These messages should be relatively infrequent and may require immediate attention when they occur.
- **`FATAL`**: This level is reserved for very severe error events that may lead to the application failing. These are very infrequent and typically indicate catastrophic failure situations.

The logging level set in your configuration determines which level(s) of logging will be written to your output destination(s). For example, if you set your level to **`INFO`**, then **`TRACE`** and **`DEBUG`** messages will be ignored.

Remember, the **`log4j2.xml`** file should be in the **`src/main/resources`** directory so it can be found when your application is run.

## **Using Log4j in Your Application**

Now that you have set up your Log4j2 configuration, using Log4j in your application is quite simple. Here are the steps to do this:

### **Importing Log4j**

First, you need to import the Log4j library in your Java class. Log4j2 uses the LogManager class to produce Logger instances.

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
```

### **Creating a Logger**

Then, you create a Logger instance for your class. By convention, this logger is static, final, and named **`logger`**. The logger should be private because it is specific to the class where it is defined.

```java
private static final Logger logger = LogManager.getLogger(MyClass.class);
```

Replace **`MyClass`** with the name of your class.

### **Logging Messages**

You can now use the **`logger`** instance to log messages. Here's how you log messages at different levels:

```java
logger.trace("This is a trace message");
logger.debug("This is a debug message");
logger.info("This is an informational message");
logger.warn("This is a warning message");
logger.error("This is an error message");
logger.fatal("This is a fatal message");
```

Remember, the log level set in your **`log4j2.xml`** configuration file determines which levels of messages are logged. For example, if you set the level to **`INFO`**, then **`TRACE`** and **`DEBUG`** messages will not be logged.

### **Logging Exceptions**

Log4j2 also provides support for logging exceptions. For example, if you have a try-catch block and want to log the caught exception, you can do this:

```java
try {
    // some code that can throw an exception
} catch (Exception e) {
    logger.error("An error occurred", e);
}
```

The **`error`** method is overloaded to accept a **`Throwable`** (the parent class of all exceptions in Java), which will be logged along with the error message.
