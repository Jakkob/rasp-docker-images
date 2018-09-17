FROM resin/rpi-raspbian:latest

# Update and install Java
RUN apt-get update && apt-get install openjdk-8-jre

ENV ES_VERSION "6.4.0"

ENV BASE_URI "https://artifacts.elastic.co/downloads/elasticsearch/"
ENV PKG_URI "${BASE_URI}elasticsearch-${ES_VERSION}.deb"
ENV SHA_URI "${BASE_URI}elasticsearch-${ES_VERSION}.deb.sha512"

# Download Elasticsearch artifacts
RUN cd /tmp \
  && curl -o "elasticsearch-${ES_VERSION}.deb" -Lskj "${PKG_URI}" \
  && curl -o "elasticsearch-${ES_VERSION}.deb.sha512" -Lskj "${SHA_URI}" \
  && sha512sum -c "elasticsearch-${ES_VERSION}.deb.sha512"

RUN echo "Shoop!"

# Install Elasticsearch.
RUN dpkg -i "/tmp/elasticsearch-${ES_VERSION}.deb"

# Cleanup the apt-get cache
RUN rm -rf /tmp/* \
  && apt-get autoremove --purge -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install the `elasticsearch.yml` config file
# COPY elasticsearch.yml /etc/elasticsearch/config/

# Add Elasticsearch executables to the PATH
ENV PATH /usr/share/elasticsearch/bin:$PATH

# Export HTTP & Transport
EXPOSE 9200 9300

# Define volumes
VOLUME /var/lib/elasticsearch/data
VOLUME /var/log/elasticsearch

# Override ENTRYPOINT
ENTRYPOINT []

# Set necesary ENV vars
ENV ES_JAVA_OPTS "-Xms512m -Xmx512m"
ENV NODE_MASTER true
ENV NODE_DATA true
ENV NODE_INGEST true
ENV NUMBER_OF_MASTERS 1
ENV HTTP_ENABLE true

USER elasticsearch

# Run it!
CMD "elasticsearch"
