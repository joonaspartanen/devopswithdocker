# Part 3 submission

## 3.1

Image sizes before optimization:

```
REPOSITORY                                      TAG                 IMAGE ID            CREATED             SIZE 
backend                                         latest              9eb8438e13de        9 minutes ago       435MB
frontend                                        latest              b29ddc5d37f0        11 minutes ago      738MB
```

Frontend layers:

```
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
b29ddc5d37f0        13 minutes ago      /bin/sh -c #(nop)  ENTRYPOINT ["/bin/sh" "-c…   0B                  
a8dac6eab0df        15 minutes ago      /bin/sh -c #(nop)  ENV API_URL=http://localh…   0B                  
022ad49dfd23        15 minutes ago      /bin/sh -c #(nop)  EXPOSE 5000                  0B                  
9ddad5c685ef        15 minutes ago      /bin/sh -c npm install                          155MB               
aaa95b1a239d        15 minutes ago      /bin/sh -c #(nop) WORKDIR /app/frontend-exam…   0B                  
c94180d3ae10        15 minutes ago      /bin/sh -c git clone https://github.com/dock…   570kB               
68cae5dbca7e        15 minutes ago      /bin/sh -c apt install -y nodejs                79.9MB              
28a3ea01d910        15 minutes ago      /bin/sh -c curl -sL https://deb.nodesource.c…   29.5MB              
b880ad8aafb0        46 minutes ago      /bin/sh -c apt-get install -y curl git npm      324MB               
8c06697fb0c7        47 minutes ago      /bin/sh -c apt-get update                       25.7MB              
c567e14a1ed9        47 minutes ago      /bin/sh -c #(nop) WORKDIR /app                  0B                
```

Backend layers:

```
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
9eb8438e13de        11 minutes ago      /bin/sh -c #(nop)  ENTRYPOINT ["/bin/sh" "-c…   0B                  
1b869755938a        11 minutes ago      /bin/sh -c #(nop)  ENV FRONT_URL=http://loca…   0B                  
900fe1033684        11 minutes ago      /bin/sh -c #(nop)  EXPOSE 8000                  0B                  
865360c86604        11 minutes ago      /bin/sh -c npm install                          58.4MB              
f624daa6fa7b        11 minutes ago      /bin/sh -c #(nop) WORKDIR /app/backend-examp…   0B                  
5cd7c5b4a185        11 minutes ago      /bin/sh -c git clone https://github.com/dock…   577kB               
f42aa3f24ac6        11 minutes ago      /bin/sh -c apt install -y nodejs                103MB               
a8f32d4978ef        11 minutes ago      /bin/sh -c curl -sL https://deb.nodesource.c…   33.3MB              
10b890fa2a42        48 minutes ago      /bin/sh -c apt-get install -y curl && apt-ge…   90.6MB              
8c06697fb0c7        48 minutes ago      /bin/sh -c apt-get update                       25.7MB              
c567e14a1ed9        48 minutes ago      /bin/sh -c #(nop) WORKDIR /app                  0B        
```

Image sizes after optimization:

```
REPOSITORY                                      TAG                 IMAGE ID            CREATED             SIZE
backend                                         latest              08649e4edeee        12 seconds ago      332MB
frontend                                        latest              9e00a804fdf0        5 seconds ago       429MB
```

[Frontend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.1/frontend/Dockerfile)

[Backend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.1/backend/Dockerfile)

## 3.2

Dockerfile:

```
FROM ubuntu:16.04

ENV LC_ALL=C.UTF-8 

RUN apt-get update && apt-get install -y python3-pip wget ffmpeg && \
  pip3 install -U yle-dl && \ 
  rm -rf /var/lib/apt/lists/*

WORKDIR /app

ENTRYPOINT ["yle-dl"]
```

Command to run the container: ```docker run -it -v $(pwd):/app yle-dl https://areena.yle.fi/1-50363232```

## 3.3

[Frontend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.3/frontend/Dockerfile)

[Backend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.3/backend/Dockerfile)

## 3.4

Image sizes before the exercise (using ubuntu:16.04):

```
REPOSITORY                                      TAG                 IMAGE ID            CREATED             SIZE  
backend-sec                                     latest              359eb2f01881        16 minutes ago      333MB
frontend-sec                                    latest              696e75068bf9        16 minutes ago      429MB 
```

Final image sizes:

```
REPOSITORY                                      TAG                 IMAGE ID            CREATED              SIZE  
backend                                         alpine              3fbbc11a7053        About a minute ago   217MB 
frontend                                        alpine              eda0327f9db1        3 minutes ago        313MB 
```

[Frontend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.4/frontend/Dockerfile)

[Backend Dockerfile](https://github.com/joonaspartanen/devopswithdocker/tree/master/part_3/3.4/backend/Dockerfile)

## 3.5 

Dockerfile:

```
FROM ubuntu:16.04 as build-stage

WORKDIR /app

RUN apt-get update && apt-get install -y curl git npm && \
  curl -sL https://deb.nodesource.com/setup_10.x | bash && \
  apt install -y nodejs && git clone https://github.com/docker-hy/frontend-example-docker.git && \
  apt-get purge -y --auto-remove curl git && rm -rf /var/lib/apt/lists/*

WORKDIR /app/frontend-example-docker

RUN npm install && npm run build

FROM node:alpine

COPY --from=build-stage /app/frontend-example-docker/dist ./dist

RUN npm install -g serve && adduser -D app && chown -R app /dist

USER app

EXPOSE 5000
ENV API_URL=http://localhost:8000

ENTRYPOINT serve -s -l 5000 dist
```

Compared to the exercise 3.4, the image size has gone down from 313MB to 123MB:

```
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
frontend-ms         latest              78f918b8fe64        About a minute ago   123MB
```

## 3.6

Dockerfile before the exercise (the app from 1.15):

```
FROM ubuntu:latest

WORKDIR /usr/app/

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/joonaspartanen/react_country_app /usr/app/
RUN npm install /usr/app/

EXPOSE 3000

CMD npm start
```

Image size: 459MB

Optimized Dockerfile:

```
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
```

After the optimization, the image size went down to 119MB.

## 3.7b

### Benefits of using Docker

Docker provides an answer to a common problem in software development: why doesn't a "perfectly working" app – according to the developer – work in another environment?

The obscure reasons behind the situation might actually be really simple, such as a missing dependency, but they can difficult to solve. And, in any case, it will take some time.

What Docker provides is a stable and portable environment that guarantees that all the pieces needed to run the app are installed when running the corresponding container.

Let's focus on an example that I learned during this course. In the exercise 1.14, you are required to create a Dockerfile for [a rails project](https://github.com/docker-hy/rails-example-project). Fortunately, the project has excellent instructions:

1. "*Make sure you have a JavaScript runtime such as node installed.*"

Let's check it out:

```
$node -v
v10.15.0
```

Perfect, node seems to be installed!

2. "*If you do not have ruby installed*"

Well, I definitely have ruby installed!

```
$ruby -v
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-gnu]
```

Let's go on.

3. "*run bundle install to install all dependencies specified in the Gemfile*"


```
$bundle install

Traceback (most recent call last):
1: from /usr/local/bin/bundle:23:in `<main>'
/usr/local/bin/bundle:23:in `load': cannot load such file -- /usr/share/rubygems-integration/all/gems/bundler-1.16.1/exe/bundle (LoadError)
```

It's not working, and I wonder why...

Well, according to the instructions, I should install "*ruby version 2.6.0 with rbenv*".

Maybe now I should read instructions for rbenv and then – if everything works – get back to the configuration of the rails project. And hope for the best!

If only the project had a Dockerfile, that would allow me to build a Docker container containing Ruby 2.6.0 (use the image tag to pull the right version!) with bundler already installed, my life would be much easier...

This was just a simple example, but precisely for its simplicity, it tells a lot about the benefits of using Docker. If running a really simple and well documented app can cause serious problems and take lots of your precious time, imagine the situation with a more complex project.

Docker makes configuring a project way easier and, as this course showcases, it's really quite simple to learn.