# Lab 1 - Building and Packaging Java Application with Gradle

## Objective

Build and package a Java application using Gradle by:

- Installing Gradle
- Cloning the project
- Running unit tests
- Building the application
- Running the generated JAR file
- Verifying the application works

---

## Prerequisites

- Java JDK installed
- Gradle installed
- Git installed


Verify the installation:

```bash
java -version
gradle -v
git --version
```

![installation verification](screenshots/verify.png)

---

## Step 1: Clone the Project

```bash
git clone https://github.com/Ibrahim-Adel15/calculator-gradle.git
cd calculator-gradle
```
![clone project](screenshots/clone_project.png)

---
## Step 2: Run Unit Tests

```bash 
gradle test
```
![run unit tests](screenshots/run_unit_tests.png)

---
## Step 3: Build the Application

```bash
gradle build
```

![gradle build](screenshots/gradle_build.png)

The JAR file is generated in:

```
build/libs/calculator.jar
```

Verify:

```bash
ls build/libs
```

![verify jar](screenshots/verify_jar.png)

---
## Step 4: Run the Application & Verify it's working

```bash
java -jar build/libs/calculator.jar
```

![run jar](screenshots/run_jar.png)

---

# Project Structure

```
calculator-gradle/
│
├── build/
│   └── libs/
│       └── calculator.jar
├── src/
├── build.gradle
└── README.md
```

---

# Result

The Java application was successfully:

- Cloned
- Tested
- Built using Gradle
- Packaged into a JAR
- Executed successfully




