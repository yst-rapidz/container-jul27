FROM node:14

# env for application
ENV APP_DIR=/app APP_PORT=3000

# env for db
ENV DB_USER=root DB_PASSWORD=changeit

# change to the APP_DIR directory
WORKDIR ${APP_DIR}


# copy files and directories
ADD main.js .
ADD package.json .
ADD package-lock.json .

ADD config config
ADD public public
ADD views views

# install dependencies
RUN npm install

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT ["node", "main.js"]
