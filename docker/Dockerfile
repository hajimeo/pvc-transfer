FROM alpine:latest
RUN apk add rsync

VOLUME /srcd
VOLUME /dest

CMD rsync -apvH /srcd/ /dest/
