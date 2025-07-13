
# **Containerizing A micro service Application**

The role of this project is to containerize a react application and use containers to deploy the application as a microservice

# CREATE DOCKER-FILES 
Create Dockerfiles for both frontend and backend. 
### Create frontend dockerfile command 
`touch client/Dockerfile`

### Create backend dockerfile file
`touch backend/Dockerfile`

## Write the contents of Frontend Dockerfile
#### The build stage: Choose light weight image
`FROM node:18-alpine AS builder`

#### Create a working directory. I decided to use `/app` for simplicity
`WORKDIR /app`

#### Copy package.json and package-lock.json from the local folder to the working directory
`COPY package*.json ./`

#### Install the application dependencies. Used `npm ci` which is more faster, more reliable and clearner
`RUN npm ci`

#### Copy everything in the current directory to the current working directory which is inside the image
`COPY . .`

#### Build the app
`RUN npm run build`


 



