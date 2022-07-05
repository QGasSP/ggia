# ggia
Greenhouse Gas Impact Assessment - main repository

To run your own version of it deploy [backend](https://github.com/QGasSP/ggia-backend) 
and [frontend](https://github.com/QGasSP/ggia-frontend) on your own server or local machine.

For creating a local dataset and testing, use this excel file: [ggia-helper](doc/excel-helpers/ggia-helper.xlsm)

GGIA test version is currently hosted here: https://ggia.ulno.net

The user manual is here: [user manual](https://drive.google.com/file/d/1kz9lxrfJqlT1X0dXDyw8kD1OmkTkzYme)

To host your own version of the ggia tool, we recommend a Linux server with a working docker installation and web-server setup (like apache or nginx), 2 GB Ram and aroudn 10GB of disk space (one processor core should be enough).

To configure nginx, you can adjust our ggia.ulno.net configuration:

server.conf in /etc/nginx/conf.d:
```
server {
 server_name ggia.ulno.net www.ggia.ulno.net;

 location /api {
   proxy_pass http://ggia.ulno.net:8000;
 }

 location /calc {
   proxy_pass http://ggia.ulno.net:8000;
 }

 location / {
   proxy_pass http://ggia.ulno.net:3000;
 }


   listen 443 ssl; # managed by Certbot
   ssl_certificate /etc/letsencrypt/live/ggia.ulno.net/fullchain.pem; # managed by Certbot
   ssl_certificate_key /etc/letsencrypt/live/ggia.ulno.net/privkey.pem; # managed by Certbot
   include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
   ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
   if ($host = ggia.ulno.net) {
       return 301 https://$host$request_uri;
   } # managed by Certbot


 server_name ggia.ulno.net www.ggia.ulno.net;
   listen 80;
   return 404; # managed by Certbot

}
```
