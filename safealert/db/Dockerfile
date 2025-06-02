FROM postgres:lastest

RUN addgroup -S postgresgrp && adduser -S postgresusr -G postgresgrp

WORKDIR /var/lib/postgresql/data

ENV POSTGRES_PASSWORD=safealertgs

RUN chown -R postgres:postgres /var/lib/postgresql/data

EXPOSE 5432

