# Use an official Node.js runtime as a parent image
FROM node:18-alpine

# Set the working directory in the container to /app
WORKDIR /app/client

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the client dependencies
RUN npm install

# Copy the current directory contents into the container at /app
COPY . .

# Expose port 3000 to the outside world
EXPOSE 3000

# Define environment variable (if needed)
# ENV REACT_APP_CUSTOM_VARIABLE value

# Run the application
CMD ["npm", "start"]
