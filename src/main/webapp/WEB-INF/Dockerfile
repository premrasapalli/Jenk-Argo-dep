## -----------------------------
## Artifact build stage
## -----------------------------
FROM maven AS buildstage

WORKDIR /opt/Jenk-Argo-dep

# Copy only the files we need
COPY src/main/webapp/WEB-INF/pom.xml .
COPY src/main/webapp/WEB-INF/src ./src

# Build the project to generate the WAR
RUN mvn clean install

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
