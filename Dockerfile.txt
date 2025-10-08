# Use official Java runtime as base image
FROM openjdk:11

# Copy Java file into image
COPY src/HelloWorld.java /app/HelloWorld.java

# Set working directory
WORKDIR /app

# Compile the Java file
RUN javac HelloWorld.java

# Command to run the Java program
CMD ["java", "HelloWorld"]
