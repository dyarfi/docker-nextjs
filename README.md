# Next.JS App with Docker container

This is a NextJS React App with Docker Container - [Development Mode]

Manually :

- Create `docker-compose.yml` in your project root.
- Create `src` folder or type `$ mkdir src` in your project root.
- Create or Copy your Next.JS app inside `src` project root directory.
- Create `Dockerfile` in `src` for your project.

Directory structure :

```
.
├── README.md
├── docker-compose.yml
└── src
    ├── Dockerfile
    ├── README.md
    ├── next.config.js
    ├── package.json
    ├── pages
    ├── postcss.config.js
    ├── public
```

`./docker-compose.yml` file.

```
version: "3"
services:
  ### SETUP SERVER CONTAINER
  server:
    # Build the server from
    build:
      context: ./src
      dockerfile: Dockerfile
    # Ports expose
    expose:
      - 3000
    # Port mapping
    ports:
      - 3000:3000
    # Volumes to mount
    volumes:
      - ./src/:/app/src
      - /app/src/node_modules
      - /app/src/.next
    # Run command
    command: yarn dev
    # Restart
    restart: always

```

`./src/Dockerfile` file.

```
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
```

Type in root directory `$ docker-compose up --build` for building container.

Type `$ docker-compose up` for running container.

Open browser and hit `http://localhost:3000/` for development.

This is a carbon copy of my [Next.JS](https://nextjs-reactstrap.now.sh/) app only it was on Docker container.
Read my medium post about [Next.JS with Reactstrap](https://medium.com/@defrian.yarfi/next-js-and-reactstrap-admin-dashboard-project-e32ff3205eb2/) admin dashboard app.
