# Part 2 submission

## 2.1

docker-compose.yml:

```
version: '3'

services:
  first-volume-exercise:
    image: devopsdockeruh/first_volume_exercise
    build: .
    volumes:
      - ./logs.txt:/usr/app/logs.txt
```

Dockerfile:

```
FROM devopsdockeruh/first_volume_exercise

WORKDIR /usr/app

CMD node index.js
```

## 2.2

docker-compose.yml:

```
version: '3'

services:
  ports_exercise:
    image: devopsdockeruh/ports_exercise
    ports:
      - 80:80
```
## 2.3

docker-compose.yml:

```
version: '3'

services:
  backend:
    image: backend-example
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    ports:
      - 8000:8000
    environment:
      - FRONT_URL=http://localhost:5000
  frontend:
    image: frontend-example
    ports:
      - 5000:5000
    environment:
      - API_URL=http://localhost:8000
```

## 2.4

Run the container with ```docker-compose up -d --scale compute=3```.

## 2.5

docker-compose.yml:

```
version: '3'

services:
  backend:
    image: backend-example
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    ports: 
      - 8000:8000
    environment: 
      - FRONT_URL=http://localhost:5000
      - REDIS=redis
  frontend:
    image: frontend-example
    ports: 
      - 5000:5000
    environment: 
      - API_URL=http://localhost:8000
  redis:
    image: redis
```

## 2.6

docker-compose.yml:

```
version: '3.5'

services:
  backend:
    image: backend-example
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    ports:
      - 8000:8000
    environment:
      - FRONT_URL=http://localhost:5000
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=example
      - DB_HOST=db
    depends_on:
      - db
  frontend:
    image: frontend-example
    ports:
      - 5000:5000
    environment:
      - API_URL=http://localhost:8000
  redis:
    image: redis
  db:
    image: postgres
    restart: unless-stopped
    environment:
      POSTGRES_PASSWORD: example
      POSTGRES_USER: postgres
```
