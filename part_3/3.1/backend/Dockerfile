FROM ubuntu:16.04

WORKDIR /app
RUN apt-get update && apt-get install -y curl git && \
  curl -sL https://deb.nodesource.com/setup_10.x | bash && \
  apt install -y nodejs && git clone https://github.com/docker-hy/backend-example-docker.git && \
  apt-get purge -y --auto-remove curl git && rm -rf /var/lib/apt/lists/*

WORKDIR /app/backend-example-docker
RUN npm install && apt-get purge -y --auto-remove npm

EXPOSE 8000
ENV FRONT_URL=http://localhost:5000

ENTRYPOINT npm start