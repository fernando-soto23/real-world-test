FROM node:20.10.0 as build

WORKDIR /app

# Copy package files first to leverage Docker cache
COPY package*.json ./

RUN npm install

# Copy the rest of the project
COPY . .

RUN npm run build

# Use a lightweight Nginx image
FROM nginx:alpine

# Copy the build output to Nginx's html directory
COPY --from=build /app/build /usr/share/nginx/html

# Dynamic port configuration
CMD ["nginx", "-g", "daemon off;"]
# Expose the port Cloud Run will use
EXPOSE 8080