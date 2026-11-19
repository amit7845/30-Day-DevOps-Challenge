# Day 4 - Docker Fundamentals and Custom Image

## Objectives
- Install and configure Docker
- Run and manage containers
- Understand images and containers
- Build a custom Docker image
- Deploy an Nginx web application

## Practical Tasks Completed

1. Installed Docker Engine.
2. Ran the hello-world container.
3. Pulled and deployed Nginx.
4. Practised container stop and start.
5. Created a custom HTML application.
6. Created a Dockerfile.
7. Built image amit-devops-app:v1.
8. Started container amit1-web-app.
9. Configured port mapping 8081:80.
10. Verified application using curl and browser.
11. Checked container logs, status and resource usage.

## Dockerfile

FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80

## Important Commands

- docker ps
- docker ps -a
- docker images
- docker logs
- docker inspect
- docker stats --no-stream
- docker stop
- docker start
- docker build -t amit-devops-app:v1 .
- docker run -d --name amit1-web-app -p 8081:80 amit-devops-app:v1

## Result

Successfully built and deployed a custom Docker image.
Verified the application through the EC2 public IP and browser.

## Key Learning

Understood Docker images, containers, Dockerfiles, port mapping,
container lifecycle, logs and basic resource monitoring.
