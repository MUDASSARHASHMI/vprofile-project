# Build stage
FROM openjdk:11 AS build_image
RUN apt update && apt install maven -y
WORKDIR /app
RUN git clone https://github.com/MUDASSARHASHMI/vprofile-project.git
WORKDIR /app/vprofile-project
RUN git checkout docker && mvn install

# Runtime stage  
FROM tomcat:9-jre11
LABEL "Author"="Mudassar Hashmi"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build_image /app/vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]