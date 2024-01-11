# Use OpenJDK 8 with Alpine as it is a very small Linux distro
FROM openjdk:8-jre-alpine3.9

# Argument for specifying the JAR file
ARG JAR_FILE

# Create a group and user with ID 1000 
RUN addgroup -g 1000 appgroup && \
    adduser -D -u 1000 -G appgroup appuser

# Set working directory to /app
WORKDIR /app

# Create logs directory inside /app and give appropriate permissions to appuser
RUN mkdir -p /app/logs && chown -R appuser:appgroup /app

# Copy the packaged jar file into our docker image
COPY --chown=appuser:appgroup ${JAR_FILE} /app/app.jar

# Change the ownership and permissions of the JAR file
RUN chmod 750 /app/app.jar

# Switch to the non-root user
USER appuser

# Set the startup command to execute the jar with the PID file path argument
CMD ["java", "-Dpidfile.path=/tmp/RUNNING_PID", "-jar", "/app/app.jar"]
