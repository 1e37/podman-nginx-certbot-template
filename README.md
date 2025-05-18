# podman-nginx-certbot-template
Configuration to run nginx with certbot and chronjob for renewal.


First, create the certbot container:

sudo podman build -t certbot .

sudo podman run -it --rm --name certbot -v ${PWD}:/letsencrypt:Z -v ${PWD}/certs:/etc/letsencrypt:Z certbot bash


Then, create and run the nginx container:

