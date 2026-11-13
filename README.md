name: cloud-service-demo
description: Git and GitHub Version Control Lab
files included: index.html, README.md

what is docker: Docker is an open-source platform that uses operating system-level virtualization to bundle applications and their dependencies into lightweight, isolated packages called containers.
what is a Docker Image:Docker is an open-source platform that uses operating system-level virtualization to bundle applications and their dependencies into lightweight, isolated packages called containers.
What is a Docker container: A Docker container is a live, runnable, and isolated instance of a Docker image.
how to build and run your application using Docker: write a Dockerfile, build the Docker image, and run the container.

docker build -t cloud-service-demo:1.0 .

docker run -d --name cloud-demo-container -p 8080:80 cloud-service-demo:1.0

What Kubernetes is and why it is used: Kubernetes is a tool that runs and manages your apps for you. Instead of starting and watching containers by hand, you tell Kubernetes what you want, and it keeps everything running, fixes things that break, and adds more copies when lots of people use the app.

Purpose of a Pod, Deployment, and Service: A Pod is the small box that actually runs your app. A Deployment is the manager that keeps the right number of Pods running and replaces broken ones. A Service is the fixed address that lets users and other apps reach those Pods, even when the Pods change.

Starting Minikube and making the Docker image available: Run minikube start to create a small Kubernetes cluster on your computer. Minikube has its own separate Docker, so it can’t see images you built normally. Either run eval $(minikube docker-env) and then build your image with docker build -t myapp:1.0 ., or build it as usual and run minikube image load myapp:1.0 to copy it in. (On Windows PowerShell, use minikube docker-env | Invoke-Expression instead of the eval command.) In your Deployment YAML, set imagePullPolicy: Never or IfNotPresent so Kubernetes uses the local image instead of trying to download it.

Applying the Deployment and Service YAML files: Use kubectl apply -f deployment.yaml and then kubectl apply -f service.yaml (or kubectl apply -f . to apply every file in the folder). This tells Kubernetes to create the Pods and the Service. You can check that everything is running with kubectl get pods and kubectl get services.

Accessing the app with kubectl port-forward: Run kubectl port-forward service/my-service 8080:80, replacing my-service with your Service name and the ports with your own (local port first, then the Service port). This creates a tunnel from your computer to the app, so you can open http://localhost:8080 in your browser. Keep the terminal open while you use it, and press Ctrl+C to stop.

minikube start --driver=docker
minikube image load cloud-service-demo:1.0
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
kubectl port-forward service/cloud-service-demo 8080:80
