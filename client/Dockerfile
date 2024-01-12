# Stage 1: Build the Node.js application
FROM node:18-alpine AS build

WORKDIR /app

COPY package.json ./

# Set DNS server to Google's public DNS
RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf

RUN npm install

COPY . .

RUN npm run build

# Stage 2: Serve the application using Nginx
FROM nginx:1.21-alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
