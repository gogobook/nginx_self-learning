`/etc/nginx` 的檔案結構
```sh
/etc/nginx # ls
conf.d                  fastcgi_params.default  mime.types.default      scgi_params             win-utf
fastcgi.conf            koi-utf                 modules                 scgi_params.default
fastcgi.conf.default    koi-win                 nginx.conf              uwsgi_params
fastcgi_params          mime.types              nginx.conf.default      uwsgi_params.default
/etc/nginx # cat nginx.conf
```
```nginx
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```
預設的html 的位置`/etc/nginx/html/index.html`