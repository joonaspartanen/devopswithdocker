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
