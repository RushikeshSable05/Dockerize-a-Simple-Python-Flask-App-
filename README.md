Goal: Create a small Flask app and run it inside Docker.

Prereqs
Docker Desktop installed, basic Python.
Steps
Create project:

mkdir ~/cloud-devops-projects/project2_docker_flask
cd ~/cloud-devops-projects/project2_docker_flask


Create a basic Flask app app.py:

# app.py
from flask import Flask

app = Flask(__name__)


@app.route('/')

def hello():

    return "Hello from Dockerized Flask!"


if __name__ == '__main__':

    app.run(host='0.0.0.0', port=5000)


Create requirements.txt:

flask==2.1.0

Create Dockerfile:

FROM python:3.9-slim
WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]


Build and run:

docker build -t flask-app .
docker run --rm -p 5000:5000 flask-app

Open http://localhost:5000 — see the message.
Validate
Browser shows “Hello from Dockerized Flask!”
Cost & cleanup
Stop container (Ctrl+C), remove image: docker rmi flask-app.
README snippet
Project: Dockerized Flask App

Run: docker build -t flask-app . && docker run -p 5000:5000 flask-app
