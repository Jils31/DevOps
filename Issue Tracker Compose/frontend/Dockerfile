# Stage 1: build the static bundle with Node
FROM node:20-alpine AS build
WORKDIR /app
COPY package.json ./
RUN npm install
COPY index.html vite.config.js ./
COPY src ./src
RUN npm run build

# Stage 2: serve it with nginx, running as the unprivileged nginx image's user
FROM nginxinc/nginx-unprivileged:1.27-alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 8080
