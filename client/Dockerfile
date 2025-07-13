# This is build stage

# choose the latest image for node. The image chosen here is light weight. Am not sure whether it will run the current version of code coz ni old kiasi.

FROM node:18-alpine AS builder

# choose/create a working directory. I decided to use /app for simplicity

WORKDIR /app

# copies the files: package.json and package-lock.json from the local folder to the working directory

COPY package*.json ./


# This is to install the application dependencies. used npm ci for faster, more reliable and clearner than npm install

RUN npm ci

# we need to copy the source files

COPY . .

# then build the app

RUN npm run build



# Production stage. Am using nginx to serve the application. Have used nginx coz it's light weight and faster. 

FROM nginx:stable-alpine AS production




