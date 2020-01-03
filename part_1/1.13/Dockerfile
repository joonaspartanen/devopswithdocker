FROM openjdk:latest

WORKDIR /usr/app
COPY ./spring-example-project .
RUN ./mvnw package

EXPOSE 8080

ENTRYPOINT java -jar ./target/docker-example-1.1.3.jar
