# exp-2 Flask Docker Deployment
docker compose version
mkdir flask-docker-app
cd flask-docker-app

-app.py:
from flask import Flask
app = Flask(__name__)
@app.route('/')
def home():
    return "Welcome to Flask Docker App!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

-Dockerfile:
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

docker build -t flask-docker-app .
docker run -p 5000:5000 flask-docker-app
http://localhost:5000
docker login
docker tag flask-docker-app YOUR_USERNAME/flask-docker-app:latest
docker push YOUR_USERNAME/flask-docker-app:latest
