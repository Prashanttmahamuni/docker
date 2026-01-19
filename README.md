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
```
🌐 Port Mapping
Port mapping connects a container’s internal port to a host port.

```bash
docker run -d -p80:80 nginx
```
This maps container port 80 to host port 80, making it accessible via localhost:80.

📝 WordPress + MySQL Setup
```bash
# Run MySQL container
docker run -d \
  -e MYSQL_ROOT_PASSWORD=Pass123 \
  -e MYSQL_DATABASE=wordpressdb \
  -v /home/ec2-user/wordpressbackup:/var/lib/sql \
  --name wpsql \
  mysql

# Run WordPress container
docker run -d -p80:80 \
  -e WORDPRESS_DB_HOST=wpsql \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_NAME=wordpressdb \
  -e WORDPRESS_DB_PASSWORD=Pass123 \
  --link wpsql:mysql \
  --name wordpress \
  wordpress
```

📂 Image Save & Load
```bash
docker save -o <tar_name>.tar <image_name>  # Save image to tar file
docker load -i <tar_name>.tar               # Load image from tar file
```

🐙 Docker Hub Workflow
```bash
docker login -u <username>                  # Login using Docker Personal Access Token
docker tag <image> <username>/<repo>:<tag>  # Tag image for Docker Hub
docker push <username>/<repo>:<tag>         # Push image to Docker Hub
```

🚀 AWS ECR Workflow
Login to AWS CLI

Authenticate to ECR using AWS-generated login command
Tag and push image:

```bash
docker tag <image> <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<repo>
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<repo>
```
🔄 docker start vs docker run
Command	Description
```bash
docker run	Creates and starts a new container
docker start	Starts an existing stopped container
```

🧹 Cleanup Commands
```bash
docker stop $(docker ps -q)                 # Stop all containers
docker rm $(docker ps -aq)                  # Remove all containers
docker rmi $(docker images -aq)             # Remove all images
docker system prune -a --volumes            # Aggressive cleanup (containers, images, volum
```

