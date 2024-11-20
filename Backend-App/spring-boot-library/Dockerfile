# Stage 1: Build the JAR file using Maven
FROM maven:3.8.4-openjdk-17 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml file to the container (to resolve dependencies before copying the rest of the code)
COPY pom.xml .

# Download Maven dependencies (this is cached unless pom.xml changes)
RUN mvn dependency:go-offline

# Copy the rest of the source code to the container
COPY src /app/src

# Build the Spring Boot JAR file (skip tests for faster build)
RUN mvn clean package -DskipTests

# Stage 2: Create the final image with the JAR file
FROM openjdk:17-jdk-slim

# Set the working directory in the final container
WORKDIR /app

# Copy the JAR file from the builder stage
COPY --from=builder /app/target/spring-boot-library-0.0.1-SNAPSHOT.jar /app/spring-boot-library.jar

# Expose the port on which the application will run
EXPOSE 8080

# Command to run the JAR file when the container starts
ENTRYPOINT ["java", "-jar", "/app/spring-boot-library.jar"]

