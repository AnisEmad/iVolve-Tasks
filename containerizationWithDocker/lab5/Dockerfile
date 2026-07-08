# ---- Stage 1: Build ----
FROM maven:3.9-eclipse-temurin-17-alpine AS build

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn package

# ---- Stage 2: Run ----
FROM amazoncorretto:17-alpine3.21

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar .

USER appuser

EXPOSE 8080

CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]