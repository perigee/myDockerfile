FROM alpine:3.4
RUN apk add --no-cache nodejs git
RUN git clone https://github.com/etsy/statsd.git

ENTRYPOINT ["node", "/statsd/stats.js", "/statsd/exampleConfig.js"]