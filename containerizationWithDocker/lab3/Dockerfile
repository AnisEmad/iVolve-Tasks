FROM maven:3.9-eclipse-temurin-17-alpine

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn package

USER appuser

CMD [ "java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]

EXPOSE 8080