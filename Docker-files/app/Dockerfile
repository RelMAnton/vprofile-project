FROM openjdk:11 AS BUILD_IMAGE
LABEL "Project"="Vprofile"
LABEL "Author"="Anton"
RUN apt update && apt install maven -y
RUN git clone https://github.com/RelMAnton/vprofile-project.git
#mvn install will compile the project to WAR
RUN cd vprofile-project && git checkout docker && mvn install


FROM tomcat:9-jre11
LABEL "project"="Vprofile"
LABEL "Author"="Anton"
RUN rm -rf /usr/local/tomcat/webapps/*
#vprofile.war will be changed to ROOT.war to be used for starting a server
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
#it will start the server
CMD ["catalina.sh", "run"]