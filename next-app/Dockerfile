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

# Build the React application
RUN npm run build

# Use a smaller, production-ready image
FROM nginx:latest

# Copy the built React app to the NGINX web root directory
COPY --from=builder /app/.next/server/app /usr/share/nginx/html
COPY --from=builder /app/.next /usr/share/nginx/html/_next

# Expose port 80
EXPOSE 80

# Command to start NGINX
CMD ["nginx", "-g", "daemon off;"]
