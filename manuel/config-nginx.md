upstream hydro-dex-web {
    server theexchange.site;
}

upstream hydro-dex-api {
    server theexchange.site;
}

upstream hydro-dex-ws {
    server theexchange.site;
}

 upstream hydro-dex-rpc {
     server theexchange.site;
 }

proxy_set_header Host              $http_host;
proxy_set_header X-Real-IP         $remote_addr;
proxy_set_heupstream hydro-dex-web {
    server theexchange.site;
}

upstream hydro-dex-api {
    server theexchange.site;
}

upstream hydro-dex-ws {
    server theexchange.site;
}

 upstream hydro-dex-rpc {
     server theexchange.site;
 }

proxy_set_header Host              $http_host;
proxy_set_header X-Real-IP         $remote_addr;
proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;

server {
    listen 80;
    server_name theexchange.site;

    # cache static content
    location ^~ /static/ {
        expires    7d;
        proxy_pass http://hydro-dex-web;
    }

    location / {
        proxy_pass http://hydro-dex-web;
    }
}

server {
    listen 80;
    server_name api.theexchange.site;
    location / {
        proxy_pass http://hydro-dex-api;
    }
}

server {
    listen 80;
    server_name ws.theexchange.site;
    location / {
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_pass http://hydro-dex-ws;
    }
}
server {
     listen 80;
     server_name rpc.theexchange.site;
     location / {
         proxy_pass http://hydro-dex-rpc;
     }
 }

    location / {
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_pass http://hydro-dex-ws;
    }
}
server {
     listen 80;
     server_name rpc.theexchange.site;
     location / {
         proxy_pass http://hydro-dex-rpc;
     }
 }
