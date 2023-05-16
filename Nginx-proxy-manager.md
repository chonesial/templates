# Nginx Proxy Manager 

## installation 

1. Install Docker and Docker Compose 
2. Install npm 

create a docker-compose.yml

```

version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt


```


visit localhostip:81 on url , for accessing the ui 

Default admin user:

Email: admin@example.com
Password: changeme


