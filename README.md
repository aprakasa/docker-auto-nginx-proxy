# Nginx Auto Proxy Server

[Docker Nginx with dynamic modules](https://github.com/nginxinc/docker-nginx/tree/master/modules) that automatically add a proxy server for available running containers.


## Command 

Clone and navigate to current directory:

```bash
git clone git@github.com:aprakasa/docker-auto-nginx-proxy && \
cd docker-auto-nginx-proxy
```

Get nginx template:

```
curl https://raw.githubusercontent.com/nginx-proxy/nginx-proxy/main/nginx.tmpl > nginx.tmpl
```

Setup `nginx-proxy` network:

```bash
docker network create nginx-proxy
```

Run the container:

```bash
docker-compose up -d
```

Clean up docker:

```bash
docker system prune -af
```

Docker images:

```bash
REPOSITORY                  TAG       IMAGE ID       CREATED       SIZE
nginx-proxy_nginx-proxy     latest    cdc0409102b3   2 hours ago   24MB
nginxproxy/acme-companion   latest    c77b599f283d   6 days ago    26.2MB
nginxproxy/docker-gen       latest    91c788cb3cb9   6 days ago    17.7MB
```

## Project Setup

Add environment for each container block:

```yml
    environment:
      VIRTUAL_PORT: ${PORT}
      VIRTUAL_HOST: ${VIRTUAL_HOST}
      LETSENCRYPT_HOST: ${LETSENCRYPT_HOST}
      LETSENCRYPT_EMAIL: ${LETSENCRYPT_EMAIL}
```
Add network at docker-compose.yml:

```yml
networks:
    default:
        external:
            name: nginx-proxy
```

## Tech
 - [Docker Nginx](https://github.com/nginxinc/docker-nginx/tree/master/modules)
 - [Brotli](https://github.com/google/brotli)
 - [Headers More](https://github.com/openresty/headers-more-nginx-module)
 - [Docker Gen](https://github.com/nginx-proxy/docker-gen)
 - [Nginx Proxy](https://github.com/nginx-proxy/nginx-proxy)
 - [ACME Companion](https://github.com/nginx-proxy/acme-companion)