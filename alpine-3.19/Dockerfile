FROM    alpine:3.19

USER    root

ENV     TZ=UTC

RUN     mkdir -p /etc/periodic/1min \
        && mkdir -p /etc/periodic/5min \
        && mkdir -p /etc/periodic/15min \
        && mkdir -p /etc/periodic/20min \
        && mkdir -p /etc/periodic/30min \
        && mkdir -p /etc/periodic/hourly \
        && mkdir -p /etc/periodic/daily \
        && mkdir -p /etc/periodic/weekly \
        && mkdir -p /etc/periodic/monthly \
        && echo "*       *       *       *       *       run-parts /etc/periodic/1min" >> /etc/crontabs/root \
        && echo "*/5     *       *       *       *       run-parts /etc/periodic/5min" >> /etc/crontabs/root \
        && echo "*/20    *       *       *       *       run-parts /etc/periodic/20min" >> /etc/crontabs/root \
        && echo "*/30    *       *       *       *       run-parts /etc/periodic/30min" >> /etc/crontabs/root \
        && apk update --no-cache \
        && apk add --update --no-cache \
                curl \
                tzdata \
                nano

ENTRYPOINT chown -R root:root /etc/periodic \
        && chmod -R +x /etc/periodic \
        && crond -f -l 8