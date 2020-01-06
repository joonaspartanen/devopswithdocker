FROM node:alpine

WORKDIR /app
RUN apk add --no-cache git npm && \
  git clone https://github.com/docker-hy/backend-example-docker.git && \
  apk del git && rm -rf /var/lib/apt/lists/* && \
  adduser -D app 

WORKDIR /app/backend-example-docker

RUN npm install && apk del npm && chown -R app /app

USER app

EXPOSE 8000
ENV FRONT_URL=http://localhost:5000

ENTRYPOINT npm start