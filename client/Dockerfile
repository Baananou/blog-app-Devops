# Build environment
FROM node:12.2.0-alpine as build
WORKDIR /app

# Set environment variables
ENV PATH /app/node_modules/.bin:$PATH

# Copy package.json and install dependencies
COPY package.json /app/package.json
RUN npm install && npm cache clean --force

# Set unsafe-perm to true
RUN npm config set unsafe-perm true

# Install react-scripts globally
RUN npm install react-scripts@3.0.1 -g

# Copy the entire application
COPY . /app

# Build the application
RUN npm run build

# Production environment
FROM nginx:1.16.0-alpine
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
