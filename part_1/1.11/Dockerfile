FROM ubuntu

WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y wget && apt-get install -y curl && apt-get install -y git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY ./backend-example-docker/package*.json ./
RUN npm install
COPY ./backend-example-docker .

EXPOSE 8000

# 1.11 version
#ENTRYPOINT npm start

# 1.12 version
ENTRYPOINT FRONT_URL=http://localhost:5000 npm start