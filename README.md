# CSC 424 Final - Junior Dev Project Modernization

This is the final exam for CSC 424 and shows how to run on a local environment

## DevOps Setup

This is a simple setup and only requires a cloning and containerization


# Run via Container

## Docker

First clone the repository to your local machine.

```bash
git clone https://github.com/ValinStudent/csc424-final-exam.git
```

Running this will setup the containers.

```bash

docker compose up --build -d

```

### Verification
Once the containers are up and running, the application is available on **port 80**. Use the following URLs to verify the deployment:

* **Frontend**: [http://localhost](http://localhost) — Loads the React frontend.
* **Backend**: [http://localhost/api/ping](http://localhost/api/ping) — Returns a response from the .NET backend.

---

## Services

This project runs three containers to host the web application

* **Frontend**: This container is the React web application built with Vite that shows the heath of each container in the browser.
* **Backend**: A .NET API that handles data requests and system health checks for the frontend, and this API also for the ping-pong API response.
* **Nginx**: This container acts as a reverse proxy and is the single entry point on port 80 for the application. It routes traffic to the correct container based on the URL it recieves.

## CI/CD Pipeline Mechanics
Automation of the integration and deployment is managed automatically with a Github Actions workflow that is located at `.github/workflows/deploy-qa.yml'

### Pipeline

* **Trigger**: This starts the process when code is pushed to main branch of the repository.
* **Build and push** This builds 3 docker images for the frontend, backend, and nginx and pushed them to Docker Hub.
* **Deployment** Using a self hosted Github Actions Runner, the new images are pulled from Docker Hub and redeployed with Docker Compose.

