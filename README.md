# I needed to maintain the contents of this file then add mine from the bottom
This is my first initial commit after forking and cloning the repository

# Create a Dockerfile
-touch Dockerfile

# create a docker-compose.yaml file
-touch docker-compose.yaml

# Created a dockerfile for both frontend and backend

# Docker file commands for frontend React APP

##Build stage
Choose the latest image which should be light weight.
-FROM node:18-alpine AS builder
 
