# AutoDeployX

A beginner DevOps project demonstrating containerized Flask application deployment using Docker.

## Tech Stack

- Python
- Flask
- Docker
- Git
- GitHub

## Features

- Simple Flask web application
- Docker containerization
- Port mapping using Docker
- Git version control
- Public GitHub repository

## Run Locally

Clone the project:

```bash
git clone https://github.com/satyamchavan-dev/autodeployx.git
```

Go to project directory:

```bash
cd autodeployx
```

Create virtual environment:

```bash
python -m venv .venv
```

Activate virtual environment:

```bash
source .venv/Scripts/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run application:

```bash
python app.py
```

## Run with Docker

Build Docker image:

```bash
docker build -t autodeployx .
```

Run Docker container:

```bash
docker run -p 5000:5000 autodeployx
```

## Output

Application runs on:

```bash
http://localhost:5000
```