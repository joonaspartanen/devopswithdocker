FROM ubuntu

WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y wget && apt-get install -y curl && apt-get install -y git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY ./frontend-example-docker/package*.json ./
RUN npm install
COPY ./frontend-example-docker .

EXPOSE 5000

ENTRYPOINT npm start