```
server {
    # Listen HTTP
    server_name ostkap-test-admin.byfl.team;


    location / {
        proxy_pass http://strapi;
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_pass_request_headers on;
    }

    listen 443 ssl http2; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/ostkap-test-admin.byfl.team/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/ostkap-test-admin.byfl.team/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = ostkap-test-admin.byfl.team) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;
    server_name ostkap-test-admin.byfl.team;
    return 404; # managed by Certbot


}

```
