FROM mysql:8.0.33
LABEL "Author"="Lex"
LABEL "Project"="vprofile"

ENV MYSQL_ROOT_PASSWORD="LexxzyDBPASS"
ENV MYSQL_DATABASE="accounts"

ADD db_backup.sql docker-entrypoint-initdb.d/db_backup.sql