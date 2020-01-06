FROM node:alpine

WORKDIR /app
RUN apk add --no-cache git npm && \
  git clone https://github.com/docker-hy/frontend-example-docker.git && \
  apk del git && rm -rf /var/lib/apt/lists/* && \
  adduser -D app

WORKDIR /app/frontend-example-docker

RUN npm install && apk del npm && chown -R app /app

USER app

EXPOSE 5000
ENV API_URL=http://localhost:8000

ENTRYPOINT npm start
