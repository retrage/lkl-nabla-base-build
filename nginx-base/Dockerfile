FROM scratch

COPY nginx.nabla /nginx.nabla
COPY data/conf /conf
COPY data/etc /etc
COPY data/www /www

ENTRYPOINT ["/nginx.nabla"]
