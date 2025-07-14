## Objective 1: Git workflow
- I have ensured strict adherence with git standards in terms of code commits with proper commit messages.
- I have also written an extensive README.md file that explains the code from the frontend, backend and docker compose files
- I have also included the images of running containers (frontend, backend and mongo containers), running networks (where mine is included [yolo-vincent-network]), successful database connectivity and docker hub images (frontend and backend images)  
- I have more than 30 commits to my repository including troubleshooting commits

## Objective 2: Image selection
 - This was a tricky one for me.
 - For the frontend image, I used node:18-alpine image which is light-weight. The final size of the container was 50.3 mb
 - For the bacend image, I still used node:18-alpine. The total image size of the container was 155mb
 - For the database image (Mongo), I used mongo:4.4 which is among the light-weight images with a total size of 425mb
 - I have used multi-stage builds to ensure that I get minimal image sizes

 ## Objective 3: Image versioning
 - all my images have been versioned as expected: Major.Minor.Patch (v1.0.0)
    - vokemwa/vincent-yolo-backend:v1.0.0
    - vokemwa/vincent-yolo-client:v1.0.0

## Objective 4: Image Deployment to Dockerhub
- All my images have been deployed to docker with proper tags
- I have attached screenshots of the images in the readme file.
- You have to deploy the containers first and they should be running
- Then I pushed my images to docker one by one through my terminal. 
- I experienced challenges with permission denied in the docker hub. I realized that I had used gooogle account to create dockerhub. I had to use username and password for it to grant me permission to push.

## Objective 5: Service Orchestration
- There was three parts to the deployment of this microservice:
  - We had the frontend application designed in ReactJS language. This application was in the /client directory with its own Dockerfile
  - The backend application designed in NodeJS with its own Dockerfile also
  - Then we had the mongoDB database that stores the data
- Each docker file is written separately with steps to depoly each application hence a microservice
- We had a docker-compose file in the root directory. The steps in this file was to:
  - Run both docker files in their respective directories
  - Create frontend container by running docker file in the /client directory, create a network and a volume
  - Create backend container by running docker file in the /backend directory, create a network and a volume
  - Create a mongodb database container
- when mapping front end port, map 3000-->80. port 80 is the default port for nginx server
- We run both containers (the three of them) and tested the application functionalities

The rest of the steps are well documented in the README file with some screenshots of whe outputs






