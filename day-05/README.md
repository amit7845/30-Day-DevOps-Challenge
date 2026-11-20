# Day 5 - Docker Volumes and Bind Mounts

## Objectives
- Understand Docker volumes
- Create and inspect named volumes
- Mount volumes into containers
- Verify data persistence
- Understand bind mounts
- Test read-only mounts

## Practical Tasks Completed

1. Created named volume devops-data.
2. Inspected Docker volume configuration.
3. Mounted volume at /data.
4. Created test.txt inside the volume.
5. Removed the original container.
6. Verified data persistence using a new container.
7. Created a host directory and HTML file.
8. Mounted host directory into Nginx.
9. Tested live file updates.
10. Verified read-only mount protection.

## Important Commands

- docker volume create devops-data
- docker volume ls
- docker volume inspect devops-data
- docker run -it --name volume-test -v devops-data:/data ubuntu:latest bash
- docker rm volume-test
- docker run --rm -v devops-data:/data ubuntu:latest cat /data/test.txt
- docker run -d --name bind-mount-app -p 8082:80 -v ~/docker-practice/website:/usr/share/nginx/html:ro nginx:latest

## Result

Successfully demonstrated Docker volume persistence after container deletion.

Successfully configured bind mounts and tested live file updates and read-only protection.

## Key Learning

Docker volumes provide persistent storage independently of containers.

Bind mounts connect host directories to containers and are useful for development workflows.
