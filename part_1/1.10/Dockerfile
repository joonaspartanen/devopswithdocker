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

# 1.10 version
#ENTRYPOINT npm start

# 1.12 version
ENTRYPOINT API_URL=http://localhost:8000 npm start