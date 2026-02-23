# Project 2
This is the second project for the course. The goal of this project is to Dockerizing an Apache web server
## Steps to Dockerize Apache Web Server
1. Create a Dockerfile
2. Build the Docker image
3. Run the Docker container
4. Access the Apache web server
### Step 1: Create a Dockerfile
Create a file named `Dockerfile` in the root directory of your project and add the following content:
```
Dockerfile
# Dockerfile for Apache Web Server
FROM alpine
#Run the command to update the package list and install Apache web server
RUN apk update && apk add apache2
#Copy the index.html file to the appropriate directory for Apache to serve
COPY ./index.html /var/www/localhost/htdocs/
EXPOSE 80
#Specify the command to start the Apache server in the foreground
# The -D FOREGROUND option tells Apache to run in the foreground, which is necessary for the container to keep running.
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"] 
# This Dockerfile uses the Alpine Linux image as the base image, which is a lightweight and minimalistic Linux distribution. It then updates the package list and installs the Apache web server. The index.html file is copied to the appropriate directory for Apache to serve. Finally, port 80 is exposed and the command to start the Apache server in the foreground is specified.
```
### Step 2: Build the Docker image
Open a terminal and navigate to the directory where the Dockerfile is located. Run the following command to build the Docker image:
```
docker build -t ahmedwalid1410/my_apache_image:latest .
```
### Step 3: Run the Docker container
After the image is built, you can run a container using the following command:
```
docker run -d -p 8080:80 --name my_apache_container ahmedwalid1410/my_apache_image:latest
```
### Step 4: Access the Apache web server
Open a web browser and navigate to `http://localhost:8080`. You should see the content of the `index.html` file that you copied to the Apache server. This means that your Apache web server is successfully Dockerized and running in a container.
## Conclusion
In this project, we have successfully Dockerized an Apache web server using a Dockerfile. We built the Docker image, ran a container, and accessed the Apache web server through a web browser. This demonstrates how Docker can be used to easily deploy and manage applications in a consistent environment.
