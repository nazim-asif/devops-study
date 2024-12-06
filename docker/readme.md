# Step creating a Dockerfile proccess
## 1. Create a Dockerfile

- Place the following Dockerfile in your project root directory (next to build.gradle or pom.xml):
```agsl

# Use an official OpenJDK runtime as a base image
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the application JAR file to the container
COPY build/libs/my-spring-boot-app.jar app.jar

# Expose the application's port
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

```


## 2. Build the Docker Image

- Run the following command in the same directory as the Dockerfile:

```agsl
docker build -t my-spring-boot-app .

```

## 3. Run the Docker Container

- Start a container using the image you just built:
```agsl
docker run -p 8080:8080 --name my-spring-boot-app-container my-spring-boot-app

```
- 8080:8080 is the port mapping format: **<local_port>:<container_port>**.

# Steps to Push the Docker Image:

- Log in to Docker Hub: Use your Docker Hub credentials to log in:

```agsl
docker login
```

- Tag the Image with Your Docker Hub Username Docker Hub requires images to be tagged with a repository name under your account. Retag your image with the correct format:

```agsl
docker tag my-spring-boot-app <your_docker_hub_username>/my-spring-boot-app:latest
```

- Push the Image Push the newly tagged image to Docker Hub:

```agsl
docker push <your_docker_hub_username>/my-spring-boot-app:latest
```