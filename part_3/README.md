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