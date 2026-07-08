# Lab 4: Run a Java Spring Boot App in a Container (JRE-only image)

## Objective
Build the Spring Boot application locally with Maven, then containerize only the
built JAR using a lightweight Java 17 base image (no Maven inside the container).
Build the image, run it, verify it works, then clean up.

## Application Source
Cloned from:
```
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
```

## Dockerfile
```dockerfile
FROM amazoncorretto:17-alpine3.21

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY target/demo-0.0.1-SNAPSHOT.jar .

USER appuser

EXPOSE 8080

CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]
```

**Design choices:**
- **Amazon Corretto 17 (Alpine)** as the base image — a JRE/JDK-only image, no
  Maven. This is much smaller than the Maven-based image used in Lab 3, since
  the app is built *outside* the container this time.
- **Non-root user**: same as Lab 3 — a dedicated `appuser`/`appgroup` runs the app
  instead of root.
- **Only the JAR is copied in** — the container never sees the source code or
  `pom.xml`, just the final build artifact.

## How This Differs From Lab 3
| | Lab 3 | Lab 4 |
|---|---|---|
| Base image | `maven:3.9-eclipse-temurin-17-alpine` | `amazoncorretto:17-alpine3.21` |
| Where the build happens | Inside the container (`mvn package`) | On the host, before `docker build` |
| What's copied in | Full source code | Just the built JAR |
| Expected image size | Larger (JDK + Maven + build cache) | Smaller (JRE + JAR only) |

## Steps & Commands

### 1. Clone the repo
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

### 2. Build the application locally with Maven
```bash
mvn package
```
![maven build](screenshots/build.png)

### 3. Verify the JAR was created
```bash
ls target
```
![verify jar](screenshots/verify.png)

### 4. Build the image (app2)
```bash
docker build -t app2 .
```
![build image](screenshots/build_image.png)

### 5. Check the image size
```bash
docker images app2
```
![image size](screenshots/size.png)

| Image | Tag    | Size |
|-------|--------|------|
| app2  | latest | *316* |

Compare this against `app1` from Lab 3 — `app2` should be noticeably smaller
since it doesn't carry Maven or the JDK build tooling, just a JRE and the jar.

### 6. Run the container
```bash
docker run -d --name container2 -p 8080:8080 app2
```
![run container](screenshots/run_container.png)

### 7. Test the application
```bash
docker ps
curl http://localhost:8080
```
![test application](screenshots/test.png)

Or open `http://localhost:8080` in a browser. Check logs if needed:
```bash
docker logs container2
```

### 8. Stop and remove the container
```bash
docker stop container2
docker rm container2
```
![stop and remove container](screenshots/stopremove.png)

## Project Structure
```
Docker-1/
│
├── target/
│   └── demo-0.0.1-SNAPSHOT.jar
├── src/
├── pom.xml
├── Dockerfile
└── README.md
```
