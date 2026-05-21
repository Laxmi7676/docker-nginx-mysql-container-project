 # Docker Core Concepts Lab

## Topics Covered
- Docker Images
- Docker Containers
- Docker Networks
- Docker Volumes
- Port Mapping
- Nginx Container
- MySQL Container
- Data Persistence

## Commands Practiced

### Pull Images
```bash
docker pull nginx
docker pull mysql:8.0
Step 2: Create a Custom Docker Network
docker network create app-network

Check network:

docker network ls
Step 3: Create Volume for MySQL Data
docker volume create mysql-data

Check volume:

docker volume ls
Step 4: Run MySQL Container
docker run -d \
--name mysql-container \
--network app-network \
-e MYSQL_ROOT_PASSWORD=root123 \
-e MYSQL_DATABASE=mydb \
-v mysql-data:/var/lib/mysql \
mysql:8.0

Explanation:

-d → run in background
--name → container name
--network → connect to custom network
-e → environment variables
-v → attach volume for persistence
Step 5: Verify MySQL Container
docker ps

Check logs:

docker logs mysql-container
Step 6: Run Nginx Container
docker run -d \
--name nginx-container \
--network app-network \
-p 8080:80 \
nginx

Explanation:

-p 8080:80
Host port = 8080
Container port = 80
Step 7: Verify Nginx

Open browser:

http://localhost:8080

You should see:

Welcome to nginx!

Step 8: Access Nginx Container
docker exec -it nginx-container bash

Inside container:

ls /usr/share/nginx/html

Exit:

exit
Step 9: Access MySQL Container
docker exec -it mysql-container mysql -u root -p

Password:

root123

Inside MySQL:

SHOW DATABASES;

Exit MySQL:

exit
Step 10: Stop and Remove Containers

Stop containers:

docker stop nginx-container mysql-container

Remove containers:

docker rm nginx-container mysql-container
Step 11: Verify Data Persistence

Run MySQL container again:

docker run -d \
--name mysql-container \
--network app-network \
-e MYSQL_ROOT_PASSWORD=root123 \
-e MYSQL_DATABASE=mydb \
-v mysql-data:/var/lib/mysql \
mysql:8.0

Your database data will still exist because of Docker volume.

Final Concepts Covered
Docker Images
Docker Containers
Docker Networks
Docker Volumes
Port Mapping
Environment Variables
Container Communication
Data Persistence
Mini Practice Tasks
Task 1

Run Apache container on port 9090.

Task 2

Create another custom network and attach containers.

Task 3

Create HTML file locally and mount it into Nginx using bind mount.

Example:

-v $(pwd)/index.html:/usr/share/nginx/html/index.html
