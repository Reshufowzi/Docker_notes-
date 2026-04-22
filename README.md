# Docker_notes-
```
FROM amazonlinux:2

# Install Apache
RUN yum update -y && \
    yum install -y httpd && \
    yum clean all

# Apache web root
WORKDIR /var/www/html

# Copy your website files
COPY . .

# Expose Apache port
EXPOSE 80

# Start Apache in foreground
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]

```
```
FROM amazonlinux:2

# Install nginx
RUN yum update -y && \
    amazon-linux-extras install nginx1 -y && \
    yum clean all

COPY . /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

# Start nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
```
```
FROM amazonlinux:2

# Install httpd, unzip, wget
RUN yum update -y && \
    yum install -y httpd unzip && \
    yum clean all

# Download template zip using ADD
ADD https://templatemo.com/download/templatemo_606_string_master /tmp/template.zip

# Unzip template and move content to Apache root
RUN unzip /tmp/template.zip -d /tmp && \
    cp -r /tmp/templatemo_606_string_master/* /var/www/html/ && \
    rm -rf /tmp/template.zip /tmp/templatemo_606_string_master

# Expose Apache port
EXPOSE 80

# Run Apache in foreground
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]

```
```
Quick Start: 3 Essential Steps 
To push an image successfully, follow these standard steps:
Log in to the Registry
Before pushing, you must authenticate. Run the following command and enter your credentials:
bash
docker login
Note: If using a private registry, specify the URL: docker login <registry-url>.
Tag Your Image
Docker images must be tagged with the destination repository name. The format is typically [REGISTRY_HOST/]username/repository:tag.
bash
docker tag local-image-name:latest your-username/remote-repo-name:v1.0
If you don't provide a tag, Docker defaults to latest.
Push the Image
Upload the tagged image to the remote repository:
bash
docker push your-username/remote-repo-name:v1.0
```

