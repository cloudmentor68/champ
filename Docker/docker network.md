### create a network

`docker network create my_nw`


### check your network

`docker network ls`


### Create two containers

`docker run -itd --name web-container --network my_nw nginx`

`docker run -itd --name app-container --network my_nw busybox sleep 3600`

### check your containers and images

`docker ps -a`

`docker images`


###  Test DNS-based communication

`docker exec -it app-container ping web-container`


### Inspect network

`docker network inspect my_nw`




------------end----------
