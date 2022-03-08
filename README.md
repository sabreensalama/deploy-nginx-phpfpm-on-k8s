# deploy-nginx-phpfpm-on-k8s

1) Create a service to expose this app, the service type must be NodePort, nodePort should be 30012.

2.) Create a config map nginx-config for nginx.conf as we want to add some custom settings for nginx.conf.

    a) Change default port 80 to 8097 in nginx.conf.

    b) Change default document root /usr/share/nginx to /var/www/html in nginx.conf.

    c) Update directory index to index index.html index.htm index.php in nginx.conf.

3.) Create a pod named nginx-phpfpm .

    b) Create a shared volume shared-files that will be used by both containers (nginx and phpfpm) also it should be a emptyDir volume.

    c) Map the ConfigMap we declared above as a volume for nginx container. Name the volume as nginx-config-volume, mount path should be /etc/nginx/nginx.conf and subPath should be nginx.conf

    d) Nginx container should be named as nginx-container and it should use nginx:latest image. PhpFPM container should be named as php-fpm-container and it should use php:7.1-fpm image.

    e) The shared volume shared-files should be mounted at /var/www/html location in both containers. Copy /opt/index.php from jump host to the nginx document root inside nginx container, once done you can access the app using App button on the top bar.
