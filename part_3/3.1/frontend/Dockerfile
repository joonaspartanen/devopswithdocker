FROM ubuntu:16.04

WORKDIR /app
RUN apt-get update && apt-get install -y curl git npm && \
  curl -sL https://deb.nodesource.com/setup_10.x | bash && \
  apt install -y nodejs && git clone https://github.com/docker-hy/frontend-example-docker.git && \
  apt-get purge -y --auto-remove curl git && rm -rf /var/lib/apt/lists/*

WORKDIR /app/frontend-example-docker
RUN npm install && apt-get purge -y --auto-remove npm


EXPOSE 5000
ENV API_URL=http://localhost:8000

ENTRYPOINT npm start
