##artifact build stage
FROM maven AS buildstage
RUN mkdir /opt/Jenk-Argo-dep
WORKDIR /opt/Jenk-Argo-dep
COPY . .
RUN mvn clean install    ## artifact -- .war

### tomcat deploy stage
FROM tomcat
WORKDIR webapps
COPY --from=buildstage /opt/Jenk-Argo-dep/target/*.war .
RUN rm -rf ROOT && mv *.war ROOT.war
EXPOSE 8080
