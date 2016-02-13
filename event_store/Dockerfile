FROM ubuntu:14.04

RUN apt-get update

RUN apt-get install -y curl

RUN curl http://download.geteventstore.com/binaries/EventStore-OSS-Ubuntu-14.04-v3.4.0.tar.gz > es.tar.gz

RUN gunzip es.tar.gz
RUN tar xf es.tar

RUN mkdir -p /etc/eventstore/

RUN cp /EventStore-OSS-Ubuntu-14.04-v3.4.0/log.config /etc/eventstore/log.config

RUN cp -r /EventStore-OSS-Ubuntu-14.04-v3.4.0 /usr/share/eventstore

# The following is taken from https://github.com/asm89/docker-event-store/blob/master/Dockerfile
# setup directory structure
ENV EVENTSTORE_OUT /var/local/EventStore/bin/eventstore/release/anycpu
ENV EVENTSTORE_BIN /var/local/EventStore/bin/eventstore/release/anycpu
ENV EVENTSTORE_DB /opt/eventstore/db
ENV EVENTSTORE_LOG /opt/eventstore/logs

# make directories
RUN mkdir -p $EVENTSTORE_BIN
RUN mkdir -p $EVENTSTORE_LOG
RUN mkdir -p $EVENTSTORE_DB

# expose LD library path
ENV LD_LIBRARY_PATH $EVENTSTORE_BIN

# export the http and tcp port
EXPOSE 2113
EXPOSE 1113

# bind it to all interfaces by default
CMD ["/usr/share/eventstore/eventstored", "--ext-ip=0.0.0.0", "--ext-http-prefixes=http://*:2113/"]
