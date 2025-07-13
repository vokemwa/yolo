# Stage1: Build
# Build Stage: Use an official Node.js runtime as a parent image
FROM node:18-alpine AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json from the host to the container
COPY package*.json ./

# Use npm ci to install only the production dependencies and perform cleanup of unnecessary files
RUN npm ci --omit=dev && npm cache clean --force

# Copies the rest of the application source code from the host to the container
COPY . .

# Stage2: Runtime

FROM node:18-alpine AS runtime

# Set the working directory inside the runtime container
WORKDIR /app

# copy everything from the /app directory in the build stage into the new runtime container
COPY --from=build /app /app

# Expose the Application port
EXPOSE 5000

# Start the server
CMD ["node", "server.js"]