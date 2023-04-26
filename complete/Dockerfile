# First stage: complete build environment
FROM ubuntu:20.04 AS MAVEN_BUILD

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y && apt-get install -y maven

COPY *.xml /app/
COPY src /app/src/

WORKDIR /app/
RUN mvn package


From openjdk:8-jre-alpine

EXPOSE 8080

RUN mkdir /app
COPY --from=MAVEN_BUILD /app/target/*.jar /app/app.jar

ENTRYPOINT ["java","-jar","/app/app.jar"]