name: cloud-service-demo
description: Git and GitHub Version Control Lab
files included: index.html, README.md

what is docker: Docker is an open-source platform that uses operating system-level virtualization to bundle applications and their dependencies into lightweight, isolated packages called containers.
what is a Docker Image:Docker is an open-source platform that uses operating system-level virtualization to bundle applications and their dependencies into lightweight, isolated packages called containers.
What is a Docker container: A Docker container is a live, runnable, and isolated instance of a Docker image.
how to build and run your application using Docker: write a Dockerfile, build the Docker image, and run the container.

docker build -t cloud-service-demo:1.0 .

docker run -d --name cloud-demo-container -p 8080:80 cloud-service-demo:1.0