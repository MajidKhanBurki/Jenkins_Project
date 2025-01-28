# Jenkins Pipeline for vProfile Project

This repository contains a Jenkins pipeline script to automate the build process for the vProfile project. The pipeline is designed to fetch the code, run unit tests, and build the project.

---

## Pipeline Overview

The pipeline uses **Maven 3.9** and **JDK 17** for building the project and consists of the following stages:

### 1. **Fetch Code**
- **Description**: Clones the `atom` branch of the vProfile project from GitHub.
- **Command Used**:
  ```groovy
  git branch: 'atom', url: 'https://github.com/hkhcoder/vprofile-project.git'
  ```

### 2. **Unit Test**
- **Description**: Runs unit tests using Maven to ensure code quality.
- **Command Used**:
  ```bash
  mvn test
  ```

### 3. **Build**
- **Description**: Builds the project and generates the `.war` artifact. Tests are skipped during this stage.
- **Command Used**:
  ```bash
  mvn install -DskipTests
  ```
- **Post Build Action**:
  - Archives the generated `.war` files for further use.
  - Command:
    ```groovy
    archiveArtifacts artifacts: '**/*.war'
    ```

---

## Prerequisites

Ensure the following tools are installed and configured on your Jenkins instance:

- **Maven 3.9**
- **JDK 17**
- Jenkins Pipeline Plugin

---

## Usage Instructions

1. **Setup the Jenkins Pipeline**:
   - Copy the pipeline script into a Jenkins pipeline project.
   - Configure the required tools (`Maven` and `JDK`) in Jenkins global tools configuration.

2. **Run the Pipeline**:
   - Trigger the pipeline to execute the stages sequentially:
     1. Fetch the project code from the `atom` branch.
     2. Run unit tests to validate the code.
     3. Build the project and archive the `.war` artifacts.

---

## Repository Details

- **GitHub URL**: [vProfile Project](https://github.com/hkhcoder/vprofile-project.git)
- **Branch Used**: `atom`

---

## Output Artifacts

The pipeline generates the following artifacts:

- **WAR File**: Available in the Jenkins workspace as `**/*.war` after a successful build.

---

## Troubleshooting

- Ensure that the `atom` branch exists in the repository.
- Verify that the correct Maven and JDK versions are configured in Jenkins.
- Check for any build or test failures in the console logs.

---