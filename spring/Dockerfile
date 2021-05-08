FROM openjdk:11-jdk

COPY /build/libs/*.jar /usr/local/app/app.jar

WORKDIR /usr/local/app

CMD ["java", "-jar", "app.jar"]