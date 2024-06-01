# Deployment

Until now, we only have seen our blog locally, but it's blog, the whole planet need to see it. Let's deploy it!

You have 2 options:

1. Serve it directly with Apache, Nginx, ...
2. Use Docker

## Apache/Nginx

If you use Apache, you just have to redirect all requests to `public/index.php`.

For Nginx, you'll need to install fastcgi. You can take inspiration from the existing `nginx.conf` file at the root of project.

## Docker

Archict comes with a Dockerfile and a docker-compose.yml to help you. The Dockerfile uses the php-fpm image, install nginx and copy Archict files. The docker-compose.yml uses this image and map port 80 to 8080. So basically you just need to run `docker compose up -d`. Feel free to update both files and even the nginx.conf file along your needs.