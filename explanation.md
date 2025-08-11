# **The IP4 at a glance**

## The ReactAPP project is supposed to be hosted in Google Kubernetes Engine (GKE)
-The project has 3 parts i.e frontend, backend and mongoDB database
-From the previous IPs, we had created a docker-compose yaml file that had created docker images and we pushed them to docker hub
-a manifest yaml file was created that combined the three parts of the application

## Frontend part of manifest file
-the front end composed of two parts:
  1. Kubernetes Deployment definition:
     - This deployment manages replicas of pods
     - This deployment makes Kubernetes run and maintain pods, each running the Docker image on port 80, and will restart them if they crash.
     - The steps are written in the manifest file
  2. Kubernetes Service definition
     - Kubernetes service exposes the frontend to the outside world
     - it's like a parmanent address for the pods that redirects traffic to the pod
     - it contains google cloud load balancer that has external IP that allows people to access the app from the internet
     - Generrally the service connects the external world to the pods i.e mapping external ports to internal pod's port
  