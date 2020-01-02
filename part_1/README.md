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