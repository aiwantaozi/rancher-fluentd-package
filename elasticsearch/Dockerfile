FROM fluent/fluentd:stable-onbuild
MAINTAINER Rancher Labs, Inc.

USER root
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories
RUN apk add --update curl jq && rm -rf /var/cache/apk/*

COPY entry.sh /usr/bin/

RUN apk add --update --virtual .build-deps \
        sudo build-base ruby-dev \

 # cutomize following instruction as you wish
 && sudo -u fluent gem install \
        fluent-plugin-elasticsearch \

 && sudo -u fluent gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem

#USER fluent

ENTRYPOINT ["/usr/bin/entry.sh"]
CMD ["fluentd", "-c", "/fluentd/etc/fluent.conf"]
