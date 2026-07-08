FROM amazoncorretto:17-alpine3.21

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY target/demo-0.0.1-SNAPSHOT.jar .

USER appuser

CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]

EXPOSE 8080