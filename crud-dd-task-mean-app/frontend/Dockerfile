FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build --prod

# Angular output fix
COPY dist/crud/ /opt/app/

FROM nginx:stable-alpine
COPY --from=build /opt/app/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
