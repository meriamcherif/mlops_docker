# Dockerized Flask App CI/CD Pipeline

This repository contains a Flask application and a GitHub Actions workflow for implementing a CI/CD pipeline. The pipeline ensures that the application is built, tested, and deployed to DockerHub.

## Features

- **Continuous Integration**:
  - Automatically builds and tests the Flask app on every push or pull request to the `main` branch.
  - Ensures all code changes are validated with `pytest`.
- **Continuous Deployment**:
  - Builds a Docker image of the application.
  - Pushes the Docker image to DockerHub upon successful completion of tests.

## Workflow Overview

### Trigger Events

The CI/CD pipeline is triggered on:
- **Push events**: When code is pushed to the `main` branch.
- **Pull requests**: When a pull request targets the `main` branch.

### Jobs in the Workflow

1. **dockerbuild**:
   - Builds the Docker image using the `DockerFile` located in the repository.

2. **build-and-test**:
   - Sets up a Python environment.
   - Installs dependencies (`Flask`, `pytest`).
   - Runs all test cases using `pytest`.

3. **build-and-publish**:
   - Logs into DockerHub using credentials stored as GitHub Secrets.
   - Builds the Docker image and pushes it to DockerHub with the tag:  
     `DOCKER_USERNAME/flasktest-app:latest`.

## Prerequisites

Before using this pipeline, ensure the following:

1. **GitHub Secrets**:
   - `DOCKER_USERNAME`: Your DockerHub username.
   - `DOCKER_PASSWORD`: Your DockerHub password or personal access token.


## How to Use

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
2. **Make changes**:
Edit the Flask app code or add/update test cases in the repository.
3. **Push changes**:
Push your changes to the main branch:
    ```bash
        git add .
        git commit -m "Your commit message"
        git push origin main

4. **Pipeline execution**:
The CI/CD pipeline will automatically:
- Build and test the application.
- Deploy the Docker image to DockerHub if all tests pass successfully.

