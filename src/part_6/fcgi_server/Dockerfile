FROM nginx:latest
USER root
RUN apt-get update && apt-get install -y \
    gcc \
    libfcgi-dev \
    spawn-fcgi && rm -rf /var/lib/apt/lists
COPY server.c /home/
COPY run.sh /home/
WORKDIR /home/
RUN chmod 777 run.sh ; \
    gcc server.c -lfcgi ; \
    chmod 777 a.out ; \
    touch /var/run/nginx.pid ; \
    chown -R nginx:nginx /var/run/nginx.pid ; \
    useradd ashlearo;
USER ashlearo
HEALTHCHECK --interval=10s --timeout=30s --start-period=5s --retries=3 CMD curl -sS 127.0.0.1 || exit 1
CMD [ "sh", "./run.sh"]