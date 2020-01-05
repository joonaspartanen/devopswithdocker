FROM ubuntu:latest

WORKDIR /usr/app/

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/joonaspartanen/react_country_app /usr/app/
RUN npm install /usr/app/

EXPOSE 3000

CMD npm start