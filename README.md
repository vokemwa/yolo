
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

#### Production stage2: For multistage builds, am using nginx to serve the application. Have used nginx coz it's light weight and faster. 

`FROM nginx:stable-alpine AS prod`

#### copy contents of the React APP build output above to the public nginx directory. It actually copies the contents of the build to the directory where nginx serves static files

`COPY --from=build /app/build /usr/share/nginx/html`


 



