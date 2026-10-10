# used older version as the newest one doesn't have curl nad i couldn't install it
FROM ubuntu:24.04

# used apt-get to remove the warning
#  `WARNING: apt does not have a stable CLI interface`
RUN apt-get update && apt-get install -y nginx

RUN sed -i 's/listen 80/listen 8080/g' /etc/nginx/sites-enabled/default

COPY index.html /var/www/html/index.html

EXPOSE 8080

# -g "daemon off;" runs nginx in the foreground, which is required for Docker so that the container still alive and not exit
CMD ["nginx", "-g", "daemon off;"]