FROM lambci/lambda:build-nodejs10.x AS node

FROM lambci/lambda:build-ruby2.5
RUN mkdir /tmp/lang /tmp/runtime
COPY --from=node /var/lang /tmp/lang
COPY --from=node /var/runtime /tmp/runtime
RUN rsync --archive --recursive /tmp/lang/ /var/lang && \
    rsync --archive --recursive /tmp/runtime/ /var/runtime && \
    rm -rf /tmp/lang /tmp/runtime
# TEMP: https://github.com/awslabs/aws-lambda-builders/pull/130
RUN sed -i 's/(".aws-sam")/(".aws-sam", ".git")/g' \
    /usr/local/lib/python2.7/site-packages/aws_lambda_builders/workflows/ruby_bundler/workflow.py
