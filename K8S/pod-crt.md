## 1. vi mypodcrt.yml

```
apiVersion: v1
kind: Pod
metadata:
  name: mywebsite-pod
spec:
  containers:
  - name: website-cont1
    image: nginx:latest
    ports:
    - containerPort: 80
```


## 2. Create pod now


```
kubectl apply -f mypodcrt.yml
```


## 3. Check pod status


```
kubectl get pods
```


## 4. Check pod details


```
kubectl describe pod mywebsite-pod
```


## 5. Access pod


```
kubectl exec -it mywebsite-pod -- /bin/bash
```


## 6. Delete pod


```
kubectl delete pod mywebsite-pod
```
