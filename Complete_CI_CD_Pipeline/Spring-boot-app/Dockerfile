FROM openjdk:21-jdk-alpine

ARG artifact=target/spring-boot-web.jar
WORKDIR /user/app

COPY ${artifact} app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
