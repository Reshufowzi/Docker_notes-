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
