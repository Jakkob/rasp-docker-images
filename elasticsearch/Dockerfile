FROM resin/rpi-raspbian:latest

# Update and install Java
RUN apt-get update && apt-get install default-jre

# Install Elasticsearch.
RUN mkdir /usr/share/elasticsearch \
  && curl -o /usr/share/elasticsearch/GPG-KEY-elasticsearch https://packages.elastic.co/GPG-KEY-elasticsearch \
  && sudo apt-get install elasticsearch

# Cleanup the apt-get cache
RUN rm -rf /tmp/* \
  && apt-get autoremove --purge -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install the `elasticsearch.yml` config file
COPY elasticsearch.yml /etc/elasticsearch/config/

# Export HTTP & Transport
EXPOSE 9200 9300

# Configure ENTRYPOINT
# COPY docker-entrypoint.sh /
# RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT []

# Run it!
CMD [ "elasticsearch" ]
