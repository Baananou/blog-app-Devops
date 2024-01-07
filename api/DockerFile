# Use an official Node.js runtime as a parent image
FROM node:18-alpine AS builder

# Set the working directory in the container to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the API dependencies
RUN npm install

# Copy the current directory contents into the container at /app
COPY . .

# Expose port 8800 to the outside world
EXPOSE 8800

# Define environment variable (if needed)
# ENV NODE_ENV production

# Run the application
CMD ["node", "start"]
