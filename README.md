# AutoDeployX

AutoDeployX is a small DevOps project I built to understand how modern application deployment actually works in real companies.

The idea behind this project was simple:
instead of manually updating an application every time code changes, I wanted to automate the complete deployment process using Jenkins and Docker.

In this project, whenever new code is pushed to GitHub, Jenkins automatically starts a pipeline, pulls the latest code, rebuilds the Docker image, stops the old container, and deploys the updated application on AWS EC2.

This project helped me practically understand Docker, Jenkins pipelines, GitHub webhooks, Linux servers, and the overall CI/CD workflow.

## Project Workflow

```text
Code Change
    ↓
Push to GitHub
    ↓
GitHub Webhook
    ↓
Jenkins Pipeline Trigger
    ↓
Docker Image Rebuild
    ↓
Old Container Stop
    ↓
New Container Deployment
    ↓
Updated Application Live on AWS
```

## Technologies Used

- Python
- Flask
- Docker
- Jenkins
- Git & GitHub
- AWS EC2
- Ubuntu Linux

## What I Learned

While building this project, I learned:

- how Docker images and containers work
- how Jenkins automates deployment
- how GitHub webhooks trigger pipelines
- how applications are deployed on AWS EC2
- how real CI/CD workflows work
- basic Linux server management

I also faced multiple real issues during development like Docker permission problems, Jenkins executor issues, webhook configuration, and disk threshold errors. Solving these problems gave me a much better understanding of real DevOps troubleshooting.

## Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/satyamchavan-dev/autodeployx.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t autodeployx .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop autodeployx-container || true'
                sh 'docker rm autodeployx-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name autodeployx-container autodeployx'
            }
        }

    }
}
```

## Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

## Running the Project Locally

Clone the repository:

```bash
git clone https://github.com/satyamchavan-dev/autodeployx.git
```

Move into the project directory:

```bash
cd autodeployx
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the Flask application:

```bash
python app.py
```

## Running with Docker

Build Docker image:

```bash
docker build -t autodeployx .
```

Run Docker container:

```bash
docker run -d -p 5000:5000 autodeployx
```

## Live Deployment

Application deployed on AWS EC2:

```text
http://44.220.190.175:5000
```

## Screenshots

- Jenkins Successful Build
- Jenkins Pipeline Stages
- GitHub Webhook Trigger
- Live Application on AWS EC2

## Final Result

By the end of this project, I successfully created a working CI/CD pipeline where every GitHub push automatically triggers Jenkins to rebuild and redeploy the Dockerized Flask application on AWS EC2.
