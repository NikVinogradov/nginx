Download zip from official site

start nginx

Verify nginx conf:
nginx -t

1) static files:
Set root path in nginx config and then you need restart
using nginx -s reload

2) Redirect
Update root path in nginx config and restart

curl localhost:80

Browser can cache this settings. You can disable cache in Dev Tools

3) Compression

    gzip on;
    gzip_types application/javascript;
    gzip_comp_level 6;

4) Proxy + Load Balancer

upstream api {
    server localhost:1111;
    server localhost:2222;
}

and change location

5) Buffer

location / {
    proxy_buffering on;
    proxy_request_buffering on;
}

6) Cache

location /api/slow_data {
    proxy_cache my_cache;
    proxy_cache_valid 200 10m;
}

7) If clients are slow
proxy_read_timeout 300;
proxy_send_timeout 300; 

8) Connection settings
worker_connections 10240;
keepalive_timeout 65;