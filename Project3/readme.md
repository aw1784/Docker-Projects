# Docker Nginx Web Server with PostgreSQL (DevOps Assignment)

This project demonstrates a basic **Dockerized web application setup** using:

- **Docker**
- **Docker Compose**
- **Nginx Web Server**
- **PostgreSQL Database**

The goal of this project is to practice **containerization, image creation, multi-container orchestration, and resource limiting**, which are core skills in **DevOps workflows**.

---

# Project Structure
Project3
│
├── Dockerfile
├── docker-compose.yml
├── myapp
│ └── index.html
└── README.md

### Description

- **Dockerfile**  
  Defines the custom image that installs **Nginx on Ubuntu** and serves a custom web page.

- **docker-compose.yml**  
  Runs a **multi-container application** consisting of:
  - Web server (Nginx)
  - PostgreSQL database
  - Persistent database storage using Docker volumes.

- **myapp/index.html**  
  Custom HTML page served by Nginx.

---

# Docker Image

The Docker image was built using:

```bash
docker build -t ahmedwalid1410/my-webserver .
```
The resulting image:

ahmedwalid1410/my-webserver:latest
- **This image contains:**

    - Ubuntu base image

    - Nginx installed

    - Custom web page
---
- **Dockerfile**
```Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y nginx

COPY myapp/index.html /var/www/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```
---
- **Running the Project with Docker Compose**

To start the full stack (web server + database):
```bash
docker compose up -d
```
- **This will start:**

    - Nginx container

    - PostgreSQL container

    - Docker volume for database persistence
---
- **docker-compose.yml**
```
services:

  web:
    image: ahmedwalid1410/my-webserver:latest
    container_name: webserver
    ports:
      - "8000:80"
    depends_on:
      - db
    deploy:
      resources:
        limits:
          cpus: "1.0"
          memory: 512M

  db:
    image: postgres
    environment:
      POSTGRES_USER: devops
      POSTGRES_PASSWORD: devops123
      POSTGRES_DB: devopsdb
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```
---
- **Accessing the Web Server**
  - Open your browser and navigate to `http://localhost:8000` to view the custom web page served by Nginx.
- **Accessing the Database**
  - You can connect to the PostgreSQL database using any PostgreSQL client with the following credentials:
    - Host: `localhost`
    - Port: `5432`
    - User: `devops`
    - Password: `devops123`
    - Database: `devopsdb`
---
# Conclusion
This project successfully demonstrates how to create a Dockerized web application using Nginx and PostgreSQL, orchestrated with Docker Compose. It highlights key DevOps practices such as containerization, multi-container orchestration, and resource management.