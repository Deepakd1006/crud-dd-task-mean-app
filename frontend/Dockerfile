# Stage 1: Build Angular app
FROM node:18-alpine AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

# Build Angular app for production
RUN npm run build -- --configuration production

# Stage 2: Nginx to serve Angular + proxy /api
FROM nginx:alpine

# Nginx config
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy built Angular files
# Using wildcard so we don't care what the project name is inside dist/
COPY --from=build /usr/src/app/dist/* /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
