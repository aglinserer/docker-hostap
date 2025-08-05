FROM ubuntu:24.04
RUN apt-get update && apt-get -y install freeradius && ln -s /etc/freeradius/3.0/ /etc/raddb
# EXPOSE map[1812/udp:{} 1813/udp:{}]
COPY raddb/ /etc/raddb/
CMD ["freeradius", "-f", "-X"]
