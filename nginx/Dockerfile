FROM debian:bullseye

RUN apt-get update && apt-get install -y \
    nginx \
    certbot \
    python3-certbot-nginx \
    supervisor \
    coreutils \
    procps \
    bash && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN groupadd nginx && useradd -r -g nginx -s /usr/sbin/nologin nginx

COPY html/ /usr/share/nginx/html
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf

COPY log-daemon/nginx-log-daemon.sh /usr/local/bin/nginx-log-daemon.sh
COPY cert/get-cert.sh /usr/local/bin/get-cert.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN chmod +x /usr/local/bin/*.sh

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]