FROM node:latest

RUN curl -o- -L https://yarnpkg.com/install.sh | bash -s

RUN mkdir -p /app/src
WORKDIR /app/src

COPY package*.json /app/src/

COPY . /app/src/

RUN yarn add next global
RUN yarn --pure-lockfile
RUN yarn install
RUN yarn cache clean

EXPOSE 3000

