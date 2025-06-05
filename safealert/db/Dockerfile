FROM postgres:15-alpine

RUN addgroup -S postgresgrp && adduser -S postgresusr -G postgresgrp

WORKDIR /var/lib/postgresql/data

ENV POSTGRES_USER=postgres
ENV POSTGRES_DB=postgres

RUN chown -R postgresusr:postgresgrp /var/lib/postgresql/data

USER postgresusr

EXPOSE 5432
