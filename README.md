# CodeAlpha Jenkins Remoting Project

**Automated CI/CD Pipeline Using Jenkins, Ubuntu WSL2, Docker and GitHub**

A hands-on DevOps project developed as part of the **CodeAlpha internship**, demonstrating Jenkins controller-agent architecture and automated application deployment using a remote Linux build agent.

## Project Overview

This project implements a Jenkins CI/CD pipeline in which a Jenkins controller running on Windows delegates build and deployment tasks to a remote Ubuntu WSL2 agent.

The pipeline retrieves a Python Flask application from GitHub, builds a Docker image, runs the application in a Docker container and automatically verifies its health.

## Architecture

```text
GitHub Repository
       |
       v
Jenkins Controller (Windows)
       |
       | WebSocket Connection
       v
Jenkins Remote Agent (Ubuntu WSL2)
       |
       v
Checkout Source Code
       |
       v
Verify Git and Docker
       |
       v
Build Docker Image
       |
       v
Run Flask Container
       |
       v
Test Application Health
       |
       v
Successful CI/CD Pipeline
```

## Technologies Used

| Technology       | Purpose                                     |
| ---------------- | ------------------------------------------- |
| Jenkins          | CI/CD automation and pipeline orchestration |
| Ubuntu WSL2      | Remote Jenkins build agent                  |
| Docker           | Application containerization                |
| Git and GitHub   | Source code management                      |
| Python and Flask | Sample web application                      |
| WebSocket        | Jenkins controller-agent communication      |
| Groovy           | Declarative Jenkins Pipeline                |

## Project Structure

```text
CodeAlpha-Jenkins-Remoting-Project/
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## CI/CD Pipeline

The Jenkins Pipeline runs on the Ubuntu remote agent and consists of four stages.

**1. Check Tools**

Verifies that Git and Docker are available on the remote agent.

**2. Build Docker Image**

Builds a Docker image containing the Flask application and its dependencies.

**3. Run Container**

Starts the Flask application inside a Docker container and maps container port 5000 to host port 5001.

**4. Test Application**

Sends an HTTP request to the application's `/health` endpoint to verify that the containerized application is responding successfully.

## Jenkins Remote Agent Configuration

The project uses a distributed Jenkins architecture:

* **Controller:** Windows 10
* **Agent:** Ubuntu running under WSL2
* **Agent label:** `ubuntu`
* **Connection:** WebSocket
* **Build environment:** Docker Desktop with WSL integration

The controller manages the Pipeline while the Ubuntu agent executes Linux shell commands and Docker operations.

## Docker Configuration

The application uses the official Python 3.12 slim image.

The Dockerfile installs Flask, copies the application source code, exposes port 5000 and starts the Flask server.

The Jenkins Pipeline builds the image using:

```bash
docker build -t codealpha-jenkins-remoting .
```

It then runs the application using:

```bash
docker run -d \
  --name codealpha-test \
  -p 5001:5000 \
  codealpha-jenkins-remoting
```

## Application Testing

After a successful build, the application is accessible at:

**Application:** `http://localhost:5001`

**Health endpoint:** `http://localhost:5001/health`

Expected health response:

```json
{
  "status": "healthy"
}
```

The Jenkins Pipeline automatically tests this endpoint and fails the build if the HTTP request is unsuccessful.

## Project Results

* Successfully connected a Windows Jenkins controller to an Ubuntu WSL2 remote agent.
* Configured Jenkins to execute Pipeline stages on the remote agent.
* Automated source code checkout from GitHub.
* Built a containerized Flask application using Docker.
* Successfully deployed and tested the application.
* Verified successful Jenkins execution and application availability.

## Screenshots

Add screenshots of your completed project here:

**1. Jenkins Remote Agent**

Show the connected Ubuntu agent in Jenkins.

**2. Successful Jenkins Pipeline**

Show the completed Pipeline with all four stages passing.

**3. Jenkins Console Output**

Show the successful Docker build and application health check. Hide any credentials, tokens or agent connection secrets.

**4. Running Flask Application**

Show the application running in your browser.

**5. Health Check**

Show the successful JSON response from `/health`.

## Key Learning Outcomes

This project provided practical experience with Jenkins distributed builds, remote agent configuration, WebSocket connectivity, Linux-based automation, Docker containerization and automated application testing.

It demonstrates how a Jenkins controller can delegate CI/CD workloads to a separate Linux environment instead of executing every task locally.

## Author

**Muhammad Fazeel Akram**

DevOps & Cloud Enthusiast

GitHub: [fazeel28329](https://github.com/fazeel28329)

Developed as part of the **CodeAlpha DevOps Internship**.
