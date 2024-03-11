FROM node:21

# create the /app directory, cd into /app
WORKDIR /app

# How to build the application
# inside /app
# copy files from local into the container
COPY main.js .
COPY package-lock.json .
COPY package.json .

COPY public public
COPY views views

# install the dependencies
RUN npm ci

# ARG: build-time variables
# ENV: run-time variables

# How to run the applicadtion
ENV APP_PORT=3000

# Tell the container what port the application needs
EXPOSE ${APP_PORT}

ENTRYPOINT node main.js