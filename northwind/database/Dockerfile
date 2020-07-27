# get mysql image from dockerhub
FROM mysql:5.7

# set root password
ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_PORT=3306

# copy the SQL files to /docker-entrypoint-initdb.d  for seeding
ADD 0-northwind-default-current-timestamp.sql /docker-entrypoint-initdb.d
ADD 1-northwind-data.sql /docker-entrypoint-initdb.d

# expose port
EXPOSE ${MYSQL_PORT}

# volume
VOLUME /var/lib/mysql

# healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 CMD mysqladmin ping -uroot -p${MYSQL_ROOT_PASSWORD} > /dev/null || exit 1
