# 🐳 Docker Deployment & Management Guide

This guide covers essential Docker commands, WordPress setup, image handling, Docker Hub workflows, and AWS ECR integration.

---

## 📦 Basic Docker Commands

```bash
docker pull <image>                         # Pull image from Docker Hub
docker images                               # List all local images
docker run -d -p80:80 <image>               # Run container in background on port 80
docker run -d -p80:80 --name <name> <image> # Run container with custom name
docker stop <container_id_or_name>          # Stop a running container
docker rm <container_id_or_name>            # Remove a container
docker exec -it <container> /bin/bash       # Open interactive shell in container
docker stop $(docker ps -q)                 # Stop all running containers
docker rm $(docker ps -aq)                  # Remove all containers
docker logs <container>                     # View container logs
docker inspect <container>                  # View detailed container info
docker image prune                          # Remove unused images
docker commit <container> <new_image>:<tag> # Create image from container

