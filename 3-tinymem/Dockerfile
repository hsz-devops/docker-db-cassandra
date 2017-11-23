# v1.0.0    2017-11-23     webmaster@highskillz.com
#
FROM cassandra:3

# ----------------------------------------------------------------------------------------
RUN \
  apt-get update && \
  apt-get install --no-install-recommends -y \
    \
    less \
    nano \
    \
    build-essential \
        python-dev \
        python-pip \
        && \
  pip install dumb-init && \
  apt-get remove -y \
        build-essential \
        python-dev \
        python-pip \
  \
  && \
  apt-get remove software-properties-common -y && \
  apt-get autoremove -y && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ----------------------------------------------------------------------------------------
COPY ./_root       /
RUN  chmod a+x     /docker-entrypoint-safedir.sh

# ----------------------------------------------------------------------------------------
# configure cassandra for minimal memory as per
#     http://opensourceconnections.com/blog/2013/08/31/building-the-perfect-cassandra-test-environment/
#
ENV MAX_HEAP_SIZE="64M"
ENV HEAP_NEWSIZE="12M"

# ----------------------------------------------------------------------------------------
ENTRYPOINT [ "/docker-entrypoint-safedir.sh" ]
CMD ["cassandra", "-f"]
