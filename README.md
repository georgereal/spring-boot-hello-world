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
- Docker containerization
- GitHub Actions CI/CD pipeline
- Automated testing and deployment

## CI/CD Pipeline

This project includes GitHub Actions workflows for continuous integration and deployment:

### Workflows

1. **CI/CD Pipeline** (`.github/workflows/ci-cd.yml`)
   - Builds and tests the application on every push and pull request
   - Runs on Ubuntu with Java 17
   - Caches Maven dependencies for faster builds
   - Uploads build artifacts

2. **Docker Build and Deploy** (`.github/workflows/docker-deploy.yml`)
   - Builds Docker image and pushes to GitHub Container Registry
   - Deploys to GitHub Pages
   - Runs on main branch pushes and releases

### Docker Support

The application can be containerized using Docker:

```bash
# Build Docker image
docker build -t spring-boot-hello-world .

# Run with Docker
docker run -p 8080:8080 spring-boot-hello-world

# Run with Docker Compose
docker-compose up -d
```

### GitHub Container Registry

Docker images are automatically published to:
`ghcr.io/georgereal/spring-boot-hello-world` 