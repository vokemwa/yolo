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

## steps for frontend service
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

## Deployment for backend

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vincent-yolo-backend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: vincent-yolo-backend
  template:
    metadata:
      labels:
        app: vincent-yolo-backend
    spec:
      containers:
        - name: vincent-yolo-backend
          image: vokemwa/vincent-yolo-backend:v1.0.0
          ports:
            - containerPort: 5000
          env:
            - name: MONGO_URL
              value: mongodb://vincent-app-ip-mongo-service:27017
```

## Steps for backend service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: vincent-yolo-backend-service
spec:
  selector:
    app: vincent-yolo-backend
  ports:
    - protocol: TCP
      port: 5000
      targetPort: 5000
```

## Persistent volume claim for mongodb databse

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```