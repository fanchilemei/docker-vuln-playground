FROM nginx:1.27-alpine@sha256:65645c7bb6a0661892a8b03b89d0743208a18dd2f3f17a54ef4b76fb8e2f2a10

# Static placeholder only. Not a vulnerable application.
COPY index.html /usr/share/nginx/html/index.html
COPY nginx.conf /etc/nginx/nginx.conf
COPY start-nginx.sh /usr/local/bin/start-nginx.sh
RUN chmod 755 /usr/local/bin/start-nginx.sh

# Non-root. Listens on 8080, so the container keeps an empty capability set.
USER nginx
EXPOSE 8080
ENTRYPOINT ["/usr/local/bin/start-nginx.sh"]
