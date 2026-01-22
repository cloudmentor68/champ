Docker Swarm is Docker’s native container orchestration tool that allows you to:

  - Run containers across multiple machines
  - Auto-scale services
  - Load balance traffic
  - Provide high availability
  - Manage containers as services

👉 Similar to Kubernetes, but simpler to start.


Docker Swarm Architecture (Simple)

   - Manager Node
     
      - Controls the cluster
      - Schedules containers

  - Worker Node

      - Runs containers

Even 1 machine can act as both `Manager + Worker`.



# Real Example: Nginx Web App with Scaling


## Step 1: Initialize Docker Swarm (Manager)


```
docker swarm init
```

Output will look like: `Swarm initialized: current node is now a manager.`


To check nodes:

```
docker node ls
```


## Step 2: Create a Service (Nginx)


```
docker service create --name web --replicas 2 -p 8080:80 nginx
```

What this does:

   - Creates a service
   - Runs 2 containers (replicas)
   - Exposes port 8080


## Step 3: Verify Service & Containers


```
docker service ls
```

```
docker service ps web
```


## Step 4: Access the Application

`alltraffic (anywhere)`

Open in browser:

`http://<SERVER-IP>:8080`


🔁 Refresh multiple times → traffic is load-balanced across replicas.


## Step 5: Scale the Service (Very Easy)

Scale from 2 → 5 containers:

```
docker service scale web=5
```

Verify:


```
docker service ps web
```

No downtime 🚀


## Step 6: Rolling Updates (Real-World Feature)

Update image version:


```
docker service update --image nginx:alpine web
```

Swarm:

   - Updates containers one by one

   - No service interruption




---------------------------------------
