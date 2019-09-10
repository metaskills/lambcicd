FROM lambci/lambda:build-nodejs8.10 AS node

FROM lambci/lambda:build-ruby2.5
RUN mkdir /tmp/lang /tmp/runtime
COPY --from=node /var/lang /tmp/lang
COPY --from=node /var/runtime /tmp/runtime
RUN rsync --archive --recursive /tmp/lang/ /var/lang && \
    rsync --archive --recursive /tmp/runtime/ /var/runtime && \
    rm -rf /tmp/lang /tmp/runtime
