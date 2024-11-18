
# Stage 1: Build the application
FROM maven:3.9.0-eclipse-temurin-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml and other necessary build files
COPY pom.xml .

# Download dependencies (this step will cache Maven dependencies)
RUN mvn dependency:go-offline -B

# Copy the rest of the application source code
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Stage 2: Run the application
FROM eclipse-temurin:17-jdk

# Set the user and working directory
USER ubuntu
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# # Expose the port your application runs on (change this if needed)
# EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

