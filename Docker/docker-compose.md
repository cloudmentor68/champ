Docker compose is used to run multiple containers using a single YAML file.

## Step 1: Install Docker & Allow permission

```
sudo apt update
sudo apt install -y docker.io
docker --version
```

```
sudo usermod -aG docker ubuntu
```


## Step 2: Install Docker Compose

```
sudo apt install docker-compose -y
docker-compose --version
```


## Step 3: Create project directory

```
mkdir docker-compose-lab
cd docker-compose-lab
```


## Step 4: Create docker-compose.yml


```
version: "3.9"

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```


## Step 5: Start the service normally


```
docker-compose up -d
```

Check running containers:

```
docker-compose ps
```


## Step 6: Scale the service

Scale to 3 containers

```
docker-compose up -d --scale web=3
```

```
docker ps -a
```

All containers use the same image but have different container names.

`❌ This will NOT work properly: Because multiple containers can’t bind to the same host port.`


## Step 7: Scaling Down

```
docker-compose up -d --scale web=1
```


## Step 8: Remove

```
docker-compose down
```



------------------------------
