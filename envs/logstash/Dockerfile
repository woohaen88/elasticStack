ARG ELK_VERSION
FROM docker.elastic.co/logstash/logstash:${ELK_VERSION}

CMD [ "/usr/share/logstash/bin/logstash", "-f", "/usr/share/logstash/config/logstash.conf"]