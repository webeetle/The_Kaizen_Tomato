FROM ubuntu:20.04

ENV DATE_TIMEZONE UTC
ENV DEBIAN_FRONTEND=noninteractive

RUN groupadd -r mysql && useradd -r -g mysql mysql

# Try to fix failures  ERROR: executor failed running [
ENV DOCKER_BUILDKIT=0
ENV COMPOSE_DOCKER_CLI_BUILD=0

RUN apt-get update && apt-get install -y \
    mysql-server \
    mysql-client \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/lib/mysql \
    && mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
    && chmod 1777 /var/lib/mysql /var/run/mysqld 

VOLUME /var/lib/mysql

COPY config/ /etc/mysql/
COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306 33060
CMD ["mysqld"]