# 🚀 Jenkins CI/CD Pipeline with GitHub & Docker

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline** using **Jenkins, GitHub, and Docker**.
The pipeline automatically pulls code from GitHub, builds a Docker image, and deploys the application on an AWS EC2 instance.

---

## 🧱 Architecture

1. Developer pushes code to GitHub
2. Jenkins pulls the latest code
3. Jenkins builds a Docker image
4. Docker container is deployed on EC2
5. Application becomes accessible via public IP

---

## 🛠️ Tech Stack

* **Jenkins** – CI/CD automation
* **Docker** – Containerization
* **GitHub** – Source code management
* **AWS EC2** – Deployment server
* **Python (Flask)** – Sample application

---

## 📁 Project Structure

```
.
├── app.py
├── requirements.txt
├── Dockerfile
└── README.md
```

---

## 📦 Application Code

### app.py

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Docker CI/CD 🚀"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

### requirements.txt

```
flask
```

---

### Dockerfile

```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

---

## ⚙️ Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/omkardgawas/devops-jenkins-ci-cd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f my-container || true
                docker run -d -p 80:5000 --name my-container my-app
                '''
            }
        }
    }
}
```

---

## 🚀 Setup Instructions

### 1. Launch EC2 Instance

* Ubuntu 22.04
* Open ports: 22, 80, 8080

### 2. Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

### 3. Run Jenkins using Docker

```bash
docker run -d \
  -p 8080:8080 \
  -p 50000:50000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name jenkins \
  jenkins/jenkins:lts
```

### 4. Configure Jenkins

* Install required plugins (Git, Pipeline)
* Create pipeline job
* Add pipeline script

---

## 🌐 Access Application

After successful pipeline execution:

```
http://<EC2-PUBLIC-IP>
eg - http://98.86.177.51
```

---

## 📊 Key Features

* Automated CI/CD pipeline
* GitHub integration
* Docker-based deployment
* Hands-on DevOps workflow
* Beginner-friendly project

---

## 🧠 Learning Outcomes

* Understanding CI/CD concepts
* Jenkins pipeline creation
* Docker containerization
* Debugging real-world issues
* AWS EC2 deployment

---

## 🚀 Future Enhancements

* Add GitHub Webhook (auto trigger)
* Use Nginx reverse proxy
* Implement multi-stage pipeline
* Deploy using Kubernetes

---

## 👨‍💻 Author

**Omkar**
DevOps Enthusiast 🚀
