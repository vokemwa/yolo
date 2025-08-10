# **Deploying ReactApp on Google Kubenetes Engine**
The role of this IP4 is to orchastrate/host the ReactAPP on Google Kubenetes Engine (GKE) so as to be reachable via internet, use stateful set to deploy mongoDB and persistent volumes.

## First, let's create a new branch for IP4 

![Images](Images/CreateIP$Branch.png)

## I had already pushed my docker images to docker hub for the frontend and backend images

![Images](Images/docker-hub-images.png)

## create a manifest.yaml file

`touch manifest.yaml`


## Front end Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vincent-yolo-client
spec:
  replicas: 2
  selector:
    matchLabels:
      app: vincent-yolo-client
  template:
    metadata:
      labels:
        app: vincent-yolo-client
    spec:
      containers:
        - name: vincent-yolo-client
          image: vokemwa/vincent-yolo-client:v1.0.0
          ports:
            - containerPort: 80

```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: vincent-yolo-client-service
spec:
  type: LoadBalancer
  selector:
    app: vincent-yolo-client
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 80
      
```