# Step 1: Build the application
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven git -y
WORKDIR /app
RUN git clone https://github.com/devopshydclub/vprofile-project.git
WORKDIR /app/vprofile-project
RUN git checkout docker && mvn clean package

# Step 2: Create the final image with Tomcat
FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Balasai"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /app/vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
