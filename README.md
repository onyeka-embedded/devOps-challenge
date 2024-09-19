# Employee Management Application

This repository contains a 3-tier employee management application designed to demonstrate DevOps processes. The application is built with a JavaScript frontend, a Node.js backend using Express, and MongoDB for data storage. It is containerized with Docker, deployed using Kubernetes (Minikube), and utilizes CI/CD pipelines for automated builds and deployments.

## Table of Contents

- [Project Overview](#project-overview)
- [DevOps Workflow](#devops-workflow)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [CI/CD Pipeline with GitHub Actions](#cicd-pipeline-with-github-actions)
- [Running the Project Locally](#running-the-project-locally)
- [Docker Setup](#docker-setup)
- [Kubernetes Deployment with Minikube](#kubernetes-deployment-with-minikube)

## Project Overview

This project showcases the DevOps lifecycle for a 3-tier employee management system. The primary focus is on:

1. **Containerization**: Dockerizing both frontend and backend services for portability and consistency across environments.
2. **CI/CD Pipelines**: Automated building, testing, and pushing Docker images to a container registry using GitHub Actions.
3. **Kubernetes Orchestration**: Deploying and managing the application using Kubernetes on Minikube.

## DevOps Workflow

1. **Code Commit**: Developers push code to GitHub.
2. **CI/CD with GitHub Actions**: A GitHub Actions pipeline is triggered to:
   - Build Docker images for both frontend and backend.
   - Run tests (if any).
   - Push Docker images to Docker Hub (or any container registry).
3. **Deployment**:
   - Use Minikube for local Kubernetes cluster setup.
   - Deploy frontend, backend, and MongoDB services using Kubernetes manifests.
   - Access the application via a Kubernetes service.

## Technologies Used

- **Frontend**: React (JavaScript)
- **Backend**: Node.js, Express
- **Database**: MongoDB
- **Containerization**: Docker
- **Orchestration**: Kubernetes (Minikube)
- **CI/CD**: GitHub Actions

## Project Structure

```bash
├── .github             # GitHub Actions workflows for CI/CD
    └── workflows       # Workflow files for building and pushing Docker images
        └── ci-cd.yml
├── frontend            # React frontend code
├── backend             # Node.js backend code
├── k8s                 # Kubernetes manifests (for Minikube deployment)
├── docker-compose.yml  # Docker Compose for local development
└── README.md           # Project documentation
```

## GitHub Actions Workflows
The .github/workflows directory contains the CI/CD pipeline definitions for:

- Building Docker images: The pipeline automates the build process using Dockerfiles for both frontend and backend services.
- Pushing to Docker Hub: The pipeline pushes the Docker images to a specified container registry (Docker Hub or private registry).
- Trigger: The pipeline is triggered on every push or pull request to the main branch.

## Running the Project Locally
Prerequisites
Ensure you have the following tools installed:

- Docker & Docker Compose
- Minikube (for Kubernetes)
- kubectl (for managing the Kubernetes cluster)
- Node.js

1. Clone the Repository
```bash
git clone https://github.com/onyeka-embedded/devOps-challenge.git
cd employee-management
```
2. Setup Environment Variables
Create an .env file in the backend directory with the following:
```bash
MONGODB_USERNAME=root
MONGODB_PASSWORD=pass
MONGODB_DATABASE= --
MONGODB_PORT=27017
-
--

PORT=5050
```
3. Run Locally With Docker
Use Docker Compose to spin up the entire application (frontend, backend, and MongoDB):
```bash
docker compose --env-file backend/.env up --build
```
* *Note the presence of --env files ./backend/.env because of the location of the .env file
You can then access the application via the following:

Frontend: http://localhost:3000

Backend API: http://localhost:5050

## Kubernetes Deployment with Minikube
1. Start Minikube
```bash
minikube start
```
2. Apply Kubernetes Manifests
The k8s directory contains the Kubernetes manifests for deploying frontend, backend, and MongoDB services.
```bash
kubectl apply -f mongodb-deploy-service.yml
kubectl apply -f backend-deploy-service.yml
kubectl apply -f frontend-deploy-service.yml
```
3. Access the Frontend
Use Minikube’s service command to expose the frontend service:
```bash
minikube service frontend-service
```
This will open the app in your default browser.

## Conclusion
This project demonstrates a full DevOps pipeline with containerized services, continuous integration and delivery using GitHub Actions, and deployment to a Kubernetes cluster via Minikube. It showcases industry-standard practices for managing microservices and cloud-native applications
