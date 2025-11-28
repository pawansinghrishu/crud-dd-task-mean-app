# Stage 1: Build Angular app
FROM node:18 AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Stage 2: Run using Nginx
FROM nginx:alpine
COPY --from=build /app/dist/dd-task-mean-app /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

