# Use an official Node runtime as a parent image
FROM node:16

# Set the working directory in the container for the frontend application
WORKDIR /app

# Copy package.json and package-lock.json (if available) from the frontend directory
COPY frontend/package*.json ./

# Install project dependencies
RUN npm install

# Bundle app source inside the docker image by copying the frontend directory
COPY frontend/ ./

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Command to run the app
CMD ["npm", "run", "serve"]
