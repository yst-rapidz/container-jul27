# the environment
# this image will be based on Node v14
FROM node:14

# create environment variables to define my workspace
ENV APP_DIR=/app APP_PORT=3000

# create and cd into APP_DIR
#   mkdir /app
#   cd /app
WORKDIR ${APP_DIR}

# copy local files into /app
#  main.js
#  package.json
ADD main.js .
ADD package.json .
ADD package-lock.json .

# copy the directories
ADD public public
ADD views views

# install dependencies
#  execute npm install
RUN npm install

# tell the container the port to be exposed
#   APP_PORT is defined in ENV line above
#   no need to EXPOSE, port will still be open based on the application itself, put it here for good practice
EXPOSE ${APP_PORT}

# run the application
#   node main.js
ENTRYPOINT ["node", "main.js"]

# Add healthcheck
#  poll every 30s
#  every failure, retry 3 times,  then failed
#  localhost because running this internally in the Docker container
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1
