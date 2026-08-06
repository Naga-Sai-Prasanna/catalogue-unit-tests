# Catalogue Microservice

The **Catalogue** service is one of the core microservices in the **Roboshop** application. It is built using **Node.js** and provides product catalogue APIs backed by MongoDB.

This repository demonstrates a complete **DevOps CI/CD workflow**, including automated unit testing, SonarQube code analysis, Docker image creation, Helm-based Kubernetes deployment, and GitOps deployment to Amazon EKS using ArgoCD.

---

# Repository Structure

```text
catalogue-unit-tests/
│
├── db/
│   └── master-data.js              # MongoDB seed data
│
├── helm/
│   ├── templates/                  # Kubernetes manifests
│   ├── Chart.yaml                  # Helm chart metadata
│   ├── values.yaml                 # Default values
│   ├── values-dev.yaml             # Development configuration
│   ├── values-uat.yaml             # UAT configuration
│   └── values-prod.yaml            # Production configuration
│
├── test/
│   └── app.test.js                 # Unit test cases
│
├── Dockerfile                      # Docker image definition
├── Jenkinsfile                     # Jenkins CI Pipeline
├── Jenkinsfile.bkp                 # Backup Jenkins pipeline
├── package.json                    # Node.js dependencies
├── server.js                       # Application entry point
├── sonar-project.properties        # SonarQube configuration
└── README.md
```

---

# Application Architecture

```text
                 Client
                    │
                    ▼
           Catalogue Service
               (Node.js)
                    │
                    ▼
                MongoDB
```

---

# CI/CD Pipeline

```text
                 Developer
                      │
                      ▼
               GitHub Repository
                      │
         GitHub Actions / Jenkins
                      │
      ┌───────────────┼────────────────┐
      │               │                │
      ▼               ▼                ▼
Install Packages   Unit Tests     SonarQube Scan
                                          │
                                          ▼
                                  Docker Build
                                          │
                                          ▼
                                  Push to Amazon ECR
                                          │
                                          ▼
                               Update Helm Values
                                          │
                                          ▼
                                      ArgoCD
                                          │
                                          ▼
                                    Amazon EKS
```

---

# Repository Components

## db/

Contains MongoDB seed data used to populate the catalogue database.

```
master-data.js
```

---

## test/

Contains automated unit tests for the application.

```
app.test.js
```

Execute the tests using:

```bash
npm test
```

---

## Dockerfile

Creates the Docker image for the Catalogue service.

Typical build process:

- Uses a Node.js base image
- Copies application source code
- Installs dependencies
- Exposes the application port
- Starts the Node.js server

Build the image:

```bash
docker build -t catalogue .
```

Run the container:

```bash
docker run -p 8080:8080 catalogue
```

---

## helm/

Contains the Helm chart used to deploy the Catalogue service into Kubernetes.

### Chart Files

- Chart.yaml
- templates/
- values.yaml

### Environment Configurations

- values-dev.yaml
- values-uat.yaml
- values-prod.yaml

This enables deploying the same application with different configurations for each environment.

Deploy using Helm:

```bash
helm install catalogue ./helm
```

---

## Jenkinsfile

Defines the Jenkins CI/CD pipeline.

Pipeline stages include:

- Source Checkout
- Install Dependencies
- Unit Testing
- SonarQube Analysis
- Docker Image Build
- Push Image to Amazon ECR
- Update Helm Values Repository

---

## package.json

Contains:

- Application metadata
- Dependencies
- Scripts
- Package versions

Install dependencies:

```bash
npm install
```

---

## server.js

Main application entry point.

Responsible for:

- Starting the HTTP server
- Handling API requests
- Connecting to MongoDB
- Serving catalogue data

Run locally:

```bash
node server.js
```

---

## sonar-project.properties

Configuration file for SonarQube.

Used during CI to perform:

- Static Code Analysis
- Code Quality Checks
- Bug Detection
- Maintainability Analysis
- Code Coverage Reporting

---

# Features

- Node.js REST API
- MongoDB Integration
- Unit Testing
- Docker Support
- Kubernetes Deployment
- Helm Charts
- SonarQube Integration
- Jenkins CI/CD
- GitHub Actions Compatible
- Amazon ECR Integration
- GitOps Deployment using ArgoCD
- Environment-specific Helm Values

---

# Technologies Used

- Node.js
- JavaScript
- MongoDB
- Docker
- Kubernetes
- Helm
- Jenkins
- GitHub Actions
- SonarQube
- Amazon ECR
- Amazon EKS
- ArgoCD

---

# Deployment Workflow

```text
Developer
    │
    ▼
Git Push
    │
    ▼
GitHub
    │
    ▼
Jenkins / GitHub Actions
    │
    ├────────► npm install
    ├────────► Unit Tests
    ├────────► SonarQube Scan
    ├────────► Docker Build
    ├────────► Push Image to Amazon ECR
    ├────────► Update Helm Values
    ▼
ArgoCD detects change
    ▼
Amazon EKS
    ▼
Catalogue Pod
```

---

# Local Development

Install dependencies:

```bash
npm install
```

Run the application:

```bash
node server.js
```

Execute unit tests:

```bash
npm test
```

Build Docker image:

```bash
docker build -t catalogue .
```

Run Docker container:

```bash
docker run -p 8080:8080 catalogue
```

Deploy to Kubernetes:

```bash
helm install catalogue ./helm
```

---

# Prerequisites

- Node.js
- npm
- Docker
- Kubernetes
- Helm
- Jenkins
- SonarQube
- AWS CLI
- Amazon ECR
- Amazon EKS

---

# Future Enhancements

- Integration Tests
- API Documentation (Swagger/OpenAPI)
- Security Scanning
- Performance Testing
- Multi-Environment Automation
- Canary Deployments

