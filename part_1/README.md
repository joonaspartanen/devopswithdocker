# Part 1 submission

## 1.1

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                          PORTS               NAMES
5c609de16221        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) About a minute ago                       stoic_perlman
9f0129ebc36d        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) About a minute ago                       elated_meitner
0d7e134f1e81        nginx               "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes                    80/tcp              nice_newton
```

## 1.2

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

## 1.3

```
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## 1.4

Commands:

```
docker exec -it epic_cartwright bash
tail -f ./logs.txt
```

Secret message:

```
Secret message is:
"Docker is easy"
Wed, 01 Jan 2020 18:28:31 GMT
```

## 1.5

Start the container:

```
docker run -d --name kontti -it ubuntu sh -c 'echo "Input website:"; read website; echo "Searc│
hing.."; sleep 1; curl http://$website;'
```

Enter the container:
```
docker exec -it kontti bash
```

Install curl inside the container:

```
apt-get update
apt-get install -y curl
```

Attach another terminal to the container:

```
docker attach --sig-proxy=false kontti
```

Input: 

```
helsinki.fi
```

Output:

```
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```

## 1.6

Create the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.6/Dockerfile) with the following content:

```
FROM devopsdockeruh/overwrite_cmd_exercise

ENTRYPOINT ["./start.sh"]
CMD ["-c"]
```

Then run ```docker build .``` in the same directory.

Tag/rename the Dockerfile with ```docker tag ac001fbf27ff docker-clock```.

The clock can now be started with ```docker run docker-clock```.

## 1.7

Create the script file as [script.sh](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.7/script.sh) and the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.7/Dockerfile) as follows:

```
FROM ubuntu

WORKDIR /mydir 

RUN apt-get update
RUN apt-get install -y curl
COPY script.sh .
RUN chmod a+rx script.sh

CMD [ "./script.sh" ]
```

Build the Dockerfile with ```docker build -t curler .```.

Run it with ```docker run -it curler```.

## 1.8

First create the logs.txt in the host folder with ```touch logs.txt```.

Now, run the container and bind the logs.txt with the command ```docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise```
 
## 1.9

Run ```docker run -d -p 80 devopsdockeruh/ports_exercise```.

Now ```docker port 0f30``` outputs:

```
80/tcp -> 0.0.0.0:32768
```

The web service can be accessed at ```http://localhost:32768/```.

## 1.10

Build the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.10/Dockerfile) with ```docker build -t frontend-example .```.

Now, run the container with ```docker run -p 5000:5000 frontend-example```.

The frontend can now be accessed at ```http://localhost:5000```.

## 1.11

First, build the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.11/Dockerfile) with ```docker build -t backend-example .```.

Before the first run, create the local [logs file](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.11/logs.txt) with ```touch logs.txt```. 

Now, run the container with ```docker run -v $(pwd)/logs.txt:/usr/src/app/logs.txt -p 8000:8000 backend-example```.

The frontend can now be accessed at ```http://localhost:8000```.

## 1.12

Modify the Dockerfile entrypoints to be ```ENTRYPOINT API_URL=http://localhost:8000 npm start``` for the [frontend](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.10/Dockerfile) and ```ENTRYPOINT FRONT_URL=http://localhost:5000 npm start``` for the [backend](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.11/Dockerfile).

Now, run both containers with the same commands as in 1.10 and 1.11.

## 1.13

Create the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.13/Dockerfile) and build it with ```docker build -t spring .```.

Then run the container with ```docker run -p 8080:8080 spring```.

## 1.14

Create the [Dockerfile](https://github.com/joonaspartanen/devopswithdocker/blob/master/part_1/1.14/Dockerfile) and build it with ```docker build -t ruby-example .```.

Then run the container with ```docker run -p 3000:3000 ruby-example```.

## 1.15

Link to the project on Docker Hub: https://hub.docker.com/repository/docker/partanenjoonas/react-country-app

## 1.16

Link to the deployed app on Heroku: https://docker-example-050120.herokuapp.com/

## 1.17

Skipped for the moment.
