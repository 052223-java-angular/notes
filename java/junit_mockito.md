# Junit & Mockito

This is a brief guide on using JUnit and Mockito for testing in Java. JUnit is a simple, open-source framework to write and run repeatable tests. Mockito is a mocking framework that tastes really good. It simplifies the development of tests for classes with external dependencies.

## **Installation**

To use JUnit and Mockito, you need to include their dependencies in your build file. If you are using Maven, add the following to your **`pom.xml`**:

```xml
<dependencies>
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.1</version>
    <scope>test</scope>
  </dependency>
  <dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>3.11.2</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

## **Writing a Simple Test**

To write a test with JUnit, you need to create a method annotated with **`@Test`**. Here's an example:

Unit testing is essential to ensure that code is working correctly. By testing individual pieces of code in isolation, developers can catch and fix issues early on in the development process. Unit tests also make it easier to refactor code, as developers can be confident that the changes they make are not introducing new bugs into the system. Ultimately, unit testing is crucial for creating high-quality and reliable software.

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class SimpleTest {
  @Test
  public void testAddition() {
    assertEquals(4, 2 + 2);
  }
}
```

The `SimpleTest` code is a basic JUnit test. It tests the `2+2` expression and asserts that the result is equal to 4. If the assertion fails, the test will fail. This test is an example of how to use JUnit to test simple expressions and values in your code.

`assertEquals` is a method in JUnit that checks if two values are equal. It takes in two arguments: the expected value and the actual value. If the values are not equal, the test will fail.

## **Mockito Basics**

Mockito allows you to create and configure mock objects. Using Mockito simplifies the development of tests for classes with external dependencies significantly.

Mock objects are objects that act like real objects in the system. They are used to test the behavior of other objects that depend on them. By creating a mock object, you can test your code without relying on the behavior of a real object or the state of a real system. When testing, mock objects are often used to replicate the behavior of objects that are difficult to set up or use in a test environment. They can also be used to keep a test separate from the effects of other parts of the system. A good example of mocking external dependencies would be a database.

Here's a simple example:

```java
import static org.mockito.Mockito.*;

public class SimpleMockTest {
  @Test
  public void testMock() {
    // Create a mock instance of the class
    List<String> mockList = mock(List.class);

    // Use the mock instance
    mockList.add("one");
    mockList.clear();

    // Verification
    verify(mockList).add("one");
    verify(mockList).clear();
  }
}
```

The mock code above is creating a mock instance of the `List` class, adding an element to it, then clearing it. It then verifies that the `add` and `clear` methods were called on the mock instance.

In the example given, the purpose of mocking the `add` and `clear` methods of the `List` object is to verify that those methods were called on the mock instance. This is a simple example to demonstrate how Mockito works. In a real-world scenario, you would typically mock more complex behavior to test the behavior of your code under a variety of conditions.

## **Mocking UserService**

Here's a basic JUnit test for the **`UserService`** class. We're using Mockito to mock the dependencies, which are **`UserDAO`** and **`RoleService`**.

```java
package com.revature.yolp.services;

import org.junit.Before;
import org.junit.Test;
import org.mindrot.jbcrypt.BCrypt;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;
import static org.junit.Assert.*;

import com.revature.yolp.daos.UserDAO;
import com.revature.yolp.models.Role;
import com.revature.yolp.models.User;

public class UserServiceTest {

    @Mock
    private UserDAO userDao;
    @Mock
    private RoleService roleService;

    private UserService userService;

    @Before
    public void setUp() {
        // Initialize the Mockito framework
        MockitoAnnotations.openMocks(this);

        // Create a new instance of the UserService class with the mocked dependencies
        userService = new UserService(userDao, roleService);
    }

    @Test
    public void testRegister() {
        // Define the test input values
        String username = "testUser";
        String password = "testPassword";
        Role role = new Role("cd7a196a-b4a1-4f2a-a6fc-902cc887ab71", "USER");
        User user = new User(username, BCrypt.hashpw(password, BCrypt.gensalt()), role.getId());

        // Mock the behavior of the roleService and userDao objects
        when(roleService.findByName("USER")).thenReturn(role);
        doNothing().when(userDao).save(any(User.class));

        // Call the register method of the userService object with the test input values
        User result = userService.register(username, password);

        // Verify that the userDao.save method was called once with any User object as
        // an argument
        verify(userDao, times(1)).save(any(User.class));

        // Verify that the result object has the expected username value
        assertEquals(username, result.getUsername());
    }
}
```

This is a Java code that tests the **`UserService`** class using JUnit and Mockito. It checks the **`register`** method by setting up the test input values, pretending to be the **`RoleService`** and **`UserDAO`** objects, and running the **`register`** method of the **`UserService`** object with the test input values. The code makes sure that the **`userDao.save`** method was called once with any **`User`** object as an argument and that the **`result`** object has the expected **`username`** value.

In the **`UserServiceTest`** class, the line `when(roleService.findByName("USER")).thenReturn(role)` is setting up Mockito to return the **`role`** object when the **`roleService.findByName("USER")`** method is called. This is because the **`register`** method of the **`UserService`** class requires a **`Role`** object with the name "USER". By mocking the **`RoleService`** object to return a **`Role`** object with the name "USER", we can test the **`register`** method without needing to use a real database.

The `doNothing().when(userDao).save(any(User.class))` line in the JUnit test for `UserService` is configuring Mockito to return nothing when the `save` method of the `UserDAO` object is called with any `User` object as an argument. This is because we don't want the `save` method to actually save anything to a real database during testing. Instead, we want to focus solely on testing the `register` method of the `UserService` class, which should be calling the `save` method at some point.

## Unit Testing UserService

```java
@Test
public void testIsValidUsername() {
    String validUsername = "validUser";
    String invalidUsername = "";

    assertTrue(userService.isValidUsername(validUsername));
    assertFalse(userService.isValidUsername(invalidUsername));
}

@Test
public void testIsUniqueUsername() {
    String existingUsername = "existingUser";
    String newUsername = "newUser";

    when(userDao.findByUsername(existingUsername)).thenReturn(Optional.of(new User()));
    when(userDao.findByUsername(newUsername)).thenReturn(Optional.empty());

    assertFalse(userService.isUniqueUsername(existingUsername));
    assertTrue(userService.isUniqueUsername(newUsername));
}

@Test
public void testIsValidPassword() {
    String validPassword = "Valid123";
    String invalidPassword = "invalid";

    assertTrue(userService.isValidPassword(validPassword));
    assertFalse(userService.isValidPassword(invalidPassword));
}

@Test
public void testIsSamePassword() {
    String password = "password123";
    String confirmPassword = "password123";
    String differentPassword = "differentPassword123";

    assertTrue(userService.isSamePassword(password, confirmPassword));
    assertFalse(userService.isSamePassword(password, differentPassword));
}
```

## **Further Reading**

- **[JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)**
- **[Mockito Documentation](https://site.mockito.org/)**
