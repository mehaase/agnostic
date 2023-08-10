FROM ubuntu:22.04
MAINTAINER mehaase@gmail.com
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y curl make mysql-server \
        postgresql sqlite3 supervisor && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
COPY tests/docker/supervisor.conf /etc/supervisor/conf.d/agnostic-tests.conf
RUN mkdir -p /var/log/supervisor

# Provide default credentials for integration tests.
ENV MYSQL_USER=root
ENV MYSQL_PASSWORD=root
ENV POSTGRES_USER=root
ENV POSTGRES_PASSWORD=root

# Set up MySQL
RUN usermod -d /var/lib/mysql/ mysql
RUN /etc/init.d/mysql start && \
    mysql -e "ALTER USER '$MYSQL_USER'@'localhost' IDENTIFIED WITH mysql_native_password BY '$MYSQL_PASSWORD';"

# Set up Postgres
# ("CREATE DATABASE" is much faster with fsync disabled:)
RUN sed --in-place 's:#fsync = on:fsync = off:' \
       /etc/postgresql/14/main/postgresql.conf

RUN /etc/init.d/postgresql start && \
    su postgres -c "echo CREATE USER root WITH SUPERUSER PASSWORD \\'root\\' | psql"

# Setup up Python
# RUN curl  https://bootstrap.pypa.io/get-pip.py | python3
RUN curl -sSL https://install.python-poetry.org | python3 -
ENV PATH="/root/.local/bin:$PATH"
RUN mkdir /opt/agnostic
COPY pyproject.toml poetry.lock README.md /opt/agnostic/
COPY src /opt/agnostic/src
WORKDIR /opt/agnostic
RUN poetry install

# This environment variable allows Click to print to stdout:
ENV LANG=C.UTF-8

# Work around weird MySQL-in-Docker error: https://serverfault.com/questions/870568/fatal-error-cant-open-and-lock-privilege-tables-table-storage-engine-for-use
VOLUME /var/lib/mysql

VOLUME /opt/agnostic
ENTRYPOINT ["/usr/bin/supervisord", "-n"]
