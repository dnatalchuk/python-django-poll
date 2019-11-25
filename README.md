## 1. Table of contents and structure
```
.
├── README.md
├── db.sqlite3
├── deployment_configs
│   ├── docker_image
│   │   └── Dockerfile
│   └── kubernetes
│       ├── deployment.yaml
│       └── service.yaml
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── polls
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   ├── 0001_initial.py
│   │   ├── __init__.py
│   ├── models.py
│   ├── static
│   │   └── polls
│   │       ├── images
│   │       │   └── sad-mac.jpg
│   │       └── style.css
│   ├── templates
│   │   └── polls
│   │       ├── detail.html
│   │       ├── index.html
│   │       └── results.html
│   ├── tests.py
│   ├── urls.py
│   └── views.py
└── requirements.txt
```

## 2. Prerequisites
Tested and deployed with the following components and versions:
```
Python 3.7.4
Docker version 19.03.4
minikube version: v1.5.2
```

## 3. How to run locally only application:
db.sqlite3 database contains added data for a simple poll for demo purposes, thus added into the repository.
* Navigate to the directory with manage.py file
```
virtualenv -p python3 ./challenge-app
source challenge-app/bin/activate
pip install -r requirements.txt
python3 manage.py runserver
```
* Navigate in browser to http://127.0.0.1:8000/polls/, a poll for voting should be available.

## 4. How to build a docker image and deploy locally minikube:
* During docker image build, setup and code will be fetched from a remote branch. To have new changes populated into a docker image, the firstly have to be committed and pushed.
* Once docker image will be built locally, Kubernetes deployment manifest will consume it locally (reflected in imagePullPolicy and extra configuration commands below);
* Kubernetes service manifest will expose locally application;
* Navigate to directory "deployment_configs/docker_image":
```
minikube start
eval $(minikube docker-env)
docker build -t challenge-app .
kubectl apply -f ../kubernetes/deployment.yaml
kubectl apply -f ../kubernetes/service.yaml
minikube service challenge-app-service
```
* In opened a browser window, navigate to /polls URL, a poll for voting should be available.