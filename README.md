# podman-nginx-certbot-template
Configuration to run nginx with certbot and chronjob for renewal.


First, create the certbot container:

sudo podman build -t certbot .

sudo podman run -it --rm --name certbot -v ${PWD}:/letsencrypt:Z -v ${PWD}/certs:/etc/letsencrypt:Z certbot bash


Same leasson for nginx:

sudo podman build -t nginx .

sudo podman run -it --rm --name nginx -v ${PWD}:/letsencrypt -v ${PWD}/certs:/etc/letsencrypt -p 80:80 -p 443:443
