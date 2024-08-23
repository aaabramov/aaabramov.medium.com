# Use the official Node.js image as the base image for building the Angular app
FROM node:20-alpine AS build

# Set the working directory inside the container to /app/src
WORKDIR /app/src

# Copy the TypeScript and Angular configuration files to the working directory
COPY tsconfig.json ./
COPY tsconfig.app.json ./
COPY angular.json ./

# Copy the package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install the application dependencies defined in package.json
RUN npm install

# Copy the rest of the application source code into the container
COPY . .

# Build the Angular application for production
RUN npm run build

# Use the official Node.js image as the base image for serving the built app
FROM node:20-alpine

# Set the working directory for the runtime environment
WORKDIR /usr/app

# Copy the built Angular app from the previous stage to the current directory
COPY --from=build /app/src/dist/hello-cloud-run ./

# Expose port 4000 to allow external access to the application
EXPOSE 4000

# Start the Node.js server in the foreground to serve the Angular application
CMD ["node", "server/server.mjs"]
