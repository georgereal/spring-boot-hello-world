# Spring Boot Hello World Application

A simple Spring Boot application that demonstrates basic REST endpoints.

## Prerequisites

- Java 17 or higher
- Maven 3.6 or higher

## Building the Application

To build the application, run:

```bash
mvn clean compile
```

## Running the Application

To run the application, use one of the following methods:

### Method 1: Using Maven
```bash
mvn spring-boot:run
```

### Method 2: Using JAR file
```bash
mvn clean package
java -jar target/helloworld-0.0.1-SNAPSHOT.jar
```

## Testing the Application

Once the application is running, you can test the endpoints:

1. **Home page**: http://localhost:8080/
   - Returns: "Welcome to Spring Boot Hello World Application!"

2. **Hello endpoint**: http://localhost:8080/hello
   - Returns: "Hello World!"

3. **Hello with custom name**: http://localhost:8080/hello?name=YourName
   - Returns: "Hello YourName!"

## Running Tests

To run the tests:

```bash
mvn test
```

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/example/helloworld/
│   │       ├── HelloworldApplication.java    # Main application class
│   │       └── HelloController.java          # REST controller
│   └── resources/
│       └── application.properties            # Application configuration
└── test/
    └── java/
        └── com/example/helloworld/
            └── HelloworldApplicationTests.java # Test class
```

## Features

- Spring Boot 3.2.0
- Spring Web starter for REST endpoints
- Maven build system
- Basic test setup
- Configurable server port (default: 8080) 