# This is build stage1

# choose the latest image. The image chosen here is light weight. Am not sure whether it will run the current version of code coz ni old kiasi.

FROM node:18-alpine AS builder

# choose/create a working directory. I decided to use /app for simplicity

WORKDIR /app

# copies the files: package.json and package-lock.json from the local folder to the working directory

COPY package*.json ./


# This is to install the application dependencies. used npm ci for faster, more reliable and clearner than npm install

RUN npm ci

# we need to copy the source files

COPY . .

# Fix webpack or openssl issues 

ENV NODE_OPTIONS=--openssl-legacy-provider

# then build the app

RUN npm run build

# Production stage2. Am using nginx to serve the application. Have used nginx coz it's light weight and faster. 

FROM nginx:stable-alpine AS prod

# copy contents of the above build output to the public directory of nginx


COPY --from=builder /app/build /usr/share/nginx/html

# Render the port nginx runs on to the application

EXPOSE 80

# there is no need to run CMD since am using the official nginx image which includes the command by default

