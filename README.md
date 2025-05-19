# podman-nginx-certbot-template
Configuration to run nginx with certbot and chronjob for renewal.


First, create the certbot container:

sudo podman build -t certbot .

sudo podman run -it --rm --name certbot -v ${PWD}:/letsencrypt:Z -v ${PWD}/certs:/etc/letsencrypt:Z certbot bash


Same  for nginx:

sudo podman build -t nginx .

sudo podman run -it --rm --name nginx -v ${PWD}:/letsencrypt -v ${PWD}/certs:/etc/letsencrypt -p 80:80 -p 443:443
sudo podman run -it --rm --name nginx -v ${PWD}:/letsencrypt -p 80:80 -p 443:443

sudo podman run -it --rm --name nginx -v ${PWD}:/letsencrypt -p 80:80 -p 443:443 nginx


#
sudo podman run -it --rm --name nginx -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf -v ${PWD}/certs:/etc/letsencrypt -p 80:80 -p 443:443 nginx


#selinux
sudo podman run -it --rm --name nginx \
  -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf:Z \
  -v ${PWD}:/letsencrypt:Z \
  -v ${PWD}/certs:/etc/letsencrypt:Z \
  -p 80:80 \
  -p 443:443 \
  nginx
  
Check Ownership and Permissions on the Host: Ensure the host directory ${PWD}/certs has the correct permissions:

ls -ld ${PWD}/certs

If the permissions are incorrect, adjust them:

chmod -R 775 ${PWD}/certs
chown -R 1002:1002 ${PWD}/certs


Verify Permissions Inside the Container: After starting the container, check if the directories are accessible:

ls -ld /etc/letsencrypt
ls -ld /letsencrypt
