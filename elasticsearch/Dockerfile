FROM resin/rpi-raspbian:latest

# Install Elasticsearch.
RUN apt-get update \
  && apt-get install default-jre \
  && mkdir /usr/share/elasticsearch \
  && wget https://packages.elastic.co/GPG-KEY-elasticsearch -O /usr/share/elasticsearch/GPG-KEY-elasticsearch \
  && sudo apt-get install elasticsearch \
  && rm -rf /tmp/* \
  && apt-get autoremove --purge -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install the `elasticsearch.yml` config file
COPY elasticsearch.yml /etc/elasticsearch/config/

# Export HTTP & Transport
EXPOSE 9200 9300

# Configure ENTRYPOINT
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

# Run it!
CMD [ "elasticsearch" ]
