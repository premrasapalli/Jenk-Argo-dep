## -----------------------------
## Artifact build stage
## -----------------------------
FROM maven:latest AS buildstage

WORKDIR /opt/Jenk-Argo-dep

# Copy the entire Maven project
COPY pom.xml .
COPY src ./src

# Build the project to generate the WAR
RUN mvn clean package

## -----------------------------
## Tomcat deployment stage
## -----------------------------
FROM tomcat:latest

WORKDIR /usr/local/tomcat/webapps

# Copy the WAR file from the Maven build stage
COPY --from=buildstage /opt/Jenk-Argo-dep/target/*.war .

# Rename WAR to ROOT.war
RUN rm -rf ROOT && mv *.war ROOT.war

EXPOSE 8080
