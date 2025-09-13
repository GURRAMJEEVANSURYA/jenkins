# Step 1: Build stage (Node.js for React/Vite)
FROM node:18 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2: Runtime stage (Tomcat for serving)
FROM tomcat:9-jdk17
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy React build output into Tomcat webapps
COPY --from=build-stage /app/dist /usr/local/tomcat/webapps/ecommerce

EXPOSE 8082
CMD ["catalina.sh", "run"]
