# Use a minimal Alpine Linux image with OpenJDK 17 as base image
FROM openjdk:17 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy the project files into the container
COPY . .

# Build the Spring Boot application using Maven
RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests
# Use a smaller base image for the final image
FROM eclipse-temurin:17-jre-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the builder stage to the final image
COPY --from=builder /app/target/*.jar app.jar

# Expose the port that your Spring Boot application will run on
EXPOSE 8082

# Specify the command to run on container startup
CMD ["java", "-jar", "app.jar", "--spring.profiles.active=container"]