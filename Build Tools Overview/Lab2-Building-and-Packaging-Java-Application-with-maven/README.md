# Lab 2 - Building and Packaging Java Application with Maven

## Objective

Build and package a Java application using Maven by:

- Installing Maven
- Cloning the project
- Running unit tests
- Building the application
- Running the generated JAR file
- Verifying the application works

---

## Prerequisites

- Java JDK installed
- Maven installed
- Git installed


Verify the installation:

```bash
java -version
mvn -v
git --version
```

![installation verification](screenshots/verify.png)

---

## Step 1: Clone the Project

```bash
git clone https://github.com/Ibrahim-Adel15/calculator-maven.git
cd calculator-maven
```
![clone project](screenshots/clone_project.png)

---
## Step 2: Run Unit Tests

```bash 
mvn test
```
![run unit tests](screenshots/run_unit_tests.png)

---
## Step 3: Build the Application

```bash
mvn package
```

![maven build](screenshots/maven_build.png)

The JAR file is generated in:
```
target/calculator.jar
```
---

Verify:

```bash
ls target
```

![verify jar](screenshots/verify_jar.png)

---
## Step 4: Run the Application & Verify it's working

```bash
java -jar target/calculator.jar
```

![run jar](screenshots/run_jar.png)

---

# Project Structure
```
calculator-maven/
│
├── target/
│   └── calculator.jar
├── src/
├── pom.xml
└── README.md
```
---

# Result

The Java application was successfully:

- Cloned
- Tested
- Built using Maven
- Packaged into a JAR
- Executed successfully
