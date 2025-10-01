## -----------------------------
## Artifact build stage
## -----------------------------
FROM maven AS buildstage

# Set working directory
WORKDIR /opt/Jenk-Argo-dep

# Copy only the folder that contains the pom.xml and source code
COPY src/main/webapp/WEB-INF/ .   # pom.xml and source code

# Build the project to generate the WAR
RUN mvn clean install

## -----------------------------
## Tomcat deployment stage
## -----------------------------
FROM tomcat:latest

# Set working directory inside Tomcat
WORKDIR /usr/local/tomcat/webapps

# Copy the WAR file from the Maven build stage
COPY --from=buildstage /opt/Jenk-Argo-dep/target/*.war .

# Rename WAR to ROOT.war
RUN rm -rf ROOT && mv *.war ROOT.war

# Expose port 8080
EXPOSE 8080

