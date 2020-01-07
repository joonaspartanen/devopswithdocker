FROM ubuntu:latest as build-stage

WORKDIR /usr/app/

RUN apt-get update && apt-get install -y curl git && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt install -y nodejs && git clone https://github.com/joonaspartanen/react_country_app /usr/app/ && \
    npm install && npm run build

FROM node:alpine

COPY --from=build-stage /usr/app/build ./build

RUN npm install -g serve && adduser -D app && chown -R app ./build

USER app

EXPOSE 3000

CMD ["serve", "-s", "-l", "3000", "build"]