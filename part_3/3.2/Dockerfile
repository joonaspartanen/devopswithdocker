FROM ubuntu:16.04

ENV LC_ALL=C.UTF-8 

RUN apt-get update && apt-get install -y python3-pip wget ffmpeg && \
  pip3 install -U yle-dl && \ 
  rm -rf /var/lib/apt/lists/*

WORKDIR /app

ENTRYPOINT ["yle-dl"]
