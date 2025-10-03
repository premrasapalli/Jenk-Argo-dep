# Build stage
FROM maven:3.9.5-eclipse-temurin-17 AS buildstage

WORKDIR /opt/Jenk-Argo-dep
COPY pom.xml .
COPY src ./src
RUN mvn clean package

# Runtime stage
FROM tomcat:10.1.14-jdk17
COPY --from=buildstage /opt/Jenk-Argo-dep/target/*.war /usr/local/tomcat/webapps/
