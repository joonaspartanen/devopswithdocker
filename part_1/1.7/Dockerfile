FROM ubuntu

WORKDIR /mydir 

RUN apt-get update
RUN apt-get install -y curl
COPY script.sh .
RUN chmod a+rx script.sh

CMD [ "./script.sh" ]
