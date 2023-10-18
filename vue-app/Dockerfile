# Use an official Node runtime as a parent image
FROM node:lts as builder

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the entire project to the container
COPY . .

# Build the Vue application
RUN npm run build

# Use a smaller, production-ready image
FROM nginx:latest

# Copy the built Vue app to the NGINX web root directory
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Command to start NGINX
CMD ["nginx", "-g", "daemon off;"]
