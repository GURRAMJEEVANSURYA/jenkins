# Stage 1: Build with Maven and Java 21
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Run with Tomcat
FROM tomcat:9.0-jdk17-temurin

# Remove default apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy backend WAR to Tomcat
COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/back1.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
