# **The IP4 at a glance**

## The ReactAPP project is supposed to be hosted in Google Kubernetes Engine (GKE)
-The project has 3 parts i.e frontend, backend and mongoDB database
-From the previous IPs, we had created a docker-compose yaml file that had created docker images and we pushed them to docker hub
-a manifest yaml file was created that combined the three parts of the application

## Frontend part of manifest file
The frontend composed of two parts:
  1. Kubernetes Deployment definition:
     - This deployment manages replicas of pods
     - This deployment makes Kubernetes run and maintain pods, each running the Docker image on port 80, and will restart them if they crash.
     - The steps are written in the manifest file
  2. Kubernetes Service definition
     - Kubernetes service exposes the frontend to the outside world
     - it's like a parmanent address for the pods that redirects traffic to the pod
     - it contains google cloud load balancer that has external IP that allows people to access the app from the internet
     - Generrally the service connects the external world to the pods i.e mapping external ports to internal pod's port


## Backend part of the manifest file
The backend is also composed of two parts:
  1. Kubernetes Deployment definition:
     - creates pods that run the backend NodeJS application
     - has pod labels which helps the frontend service to find them
     - each pod runs the image from dockerhub
     - it has an environment variable `MONGO_URL` that tells the backend where to find MongoDB

  2. Kubernetes Service definition
     - the service finds all pods with the label app=vincent-yolo-backend
     - the service listens to port 5000 inside the cluster
     - the service also forwards traffic to port 5000 on the pod

## MongoDB part of manifest file
The mongo db comprises of three parts:
  1. Kubernetes Deployment definition:
     - This deployment manages the mongodb pod and ensure it's running by recreating it if it fails
     - gives the deployment a name
     - Runs MongoDB (`version 4.4`) in a single replica pod
     - it exposes mongo DB's default port 27017 for connections inside the cluster
     - it mounts a persistent storage so that the database data doesn't get lost when the pod restarts
     - it also uses persistent volume claim to request for storage
  2. persistent volume claim for the database
     - This is a request for storage by the pod. Like give me this disk space....
     - It’s a storage request Kubernetes will fulfill so MongoDB has disk space to save data.
  3. MongoDB service
     - Exposes MongoDB on port 27017 inside the cluster
     - this service lets other pods like the backend pod to connect to MongoDB
