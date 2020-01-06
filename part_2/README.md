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

## 2.7

docker-compose.yml:

```
version: '3.5'

services:
  backend:
    build:
      context: https://github.com/docker-hy/ml-kurkkumopo-backend.git
      dockerfile: Dockerfile
    image: backend
    ports:
      - 5000:5000
    volumes:
      - model:/src/model
  frontend:
    build:
      context: https://github.com/docker-hy/ml-kurkkumopo-frontend.git
      dockerfile: Dockerfile
    image: frontend
    ports:
      - 3000:3000
  training:
    build:
      context: https://github.com/docker-hy/ml-kurkkumopo-training.git
      dockerfile: Dockerfile
    volumes:
      - imgs:/src/imgs
      - model:/src/model
volumes:
  model:
  imgs:
```

## 2.8

docker-compose.yml:

```
version: '3.5'

services:
  backend:
    image: backend-example
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=example
      - DB_HOST=db
      - FRONT_URL=http://localhost:5000
    depends_on:
      - db
    container_name: backend
  frontend:
    image: frontend-example
    container_name: frontend
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
  proxy:
    image: nginx
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    ports:
      - 80:80
    depends_on:
      - backend
      - frontend  
```

nginx.conf:

```
events { worker_connections 1024; }

http {
  server {
    listen 80;

    location / {
      proxy_pass http://frontend:5000/;
    }

    location /api/ {
      proxy_pass http://backend:8000/;
    }
  }
}
```

## 2.9

```
version: '3.5'

services:
  backend:
    image: backend-example
    volumes:
      - ./logs.txt:/usr/src/app/logs.txt
    environment:
      - REDIS=redis
      - DB_USERNAME=postgres
      - DB_PASSWORD=example
      - DB_HOST=db
      - FRONT_URL=http://localhost:5000
    ports:
      - 8000:8000
    depends_on:
      - db
    container_name: backend
  frontend:
    image: frontend-example
    container_name: frontend
    ports:
      - 5000:5000
    environment:
      - API_URL=http://localhost:8000
  redis:
    image: redis
    volumes:
      - ./redisdb:/data
  db:
    image: postgres
    restart: unless-stopped
    environment:
      POSTGRES_PASSWORD: example
      POSTGRES_USER: postgres
    volumes:
      - ./database:/var/lib/postgresql/data
volumes:
  database:
  redisdb:
```

## 2.10

Skipped for the moment.
