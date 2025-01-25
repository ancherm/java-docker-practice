FROM openjdk:8-jdk-alpine AS builder
WORKDIR /usr/src/app

RUN apk add --no-cache maven

COPY pom.xml /usr/src/app
COPY src /usr/src/app/src

RUN mvn clean package -DskipTests

FROM openjdk:8-jre-alpine
WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/target/*.jar /usr/src/app/docker-spring-boot.jar

EXPOSE 8888

ENTRYPOINT ["java", "-jar", "/usr/src/app/docker-spring-boot.jar"]