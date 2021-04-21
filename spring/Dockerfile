FROM openjdk:11-jdk

COPY ./build/libs/spring-0.0.1-SNAPSHOT.jar /usr/local/app/app.jar

WORKDIR /usr/local/app

CMD ["java", "-jar", "app.jar"]