FROM        nginx:1.17

ENV         TINI_VERSION v0.18.0

WORKDIR     /etc/nginx

COPY        root/nginx/nginx.conf /etc/nginx/nginx.conf
COPY        root/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY        root/nginx/conf.d/default_ssl.conf /etc/nginx/conf.d/default_ssl.conf

# Add Tini
ADD         https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini

RUN         chmod +x /tini && \
            if [ -z ${USE_SSL+x} ]; then rm -rf /etc/nginx/conf.d/default_ssl.conf; else rm -rf /etc/nginx/conf.d/default.conf; fi

EXPOSE      80 443
ENTRYPOINT  ["/tini", "--"]

CMD         ["nginx", "-g", "daemon off;"]