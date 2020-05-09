# FROM node:10
# FROM node:alpine
FROM node:latest

RUN curl -o- -L https://yarnpkg.com/install.sh | bash -s

RUN yarn add next global

RUN mkdir -p /app/src

WORKDIR /app/src

COPY package*.json /app/src/
# COPY yarn.* /app/src/

COPY . /app/src/

RUN yarn --pure-lockfile
RUN yarn install
# RUN yarn add --force node-sass
# RUN npm rebuild node-sass
RUN yarn cache clean

EXPOSE 3000

