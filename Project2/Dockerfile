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