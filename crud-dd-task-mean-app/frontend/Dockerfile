FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build  --omit=dev

# Auto-detect Angular dist folder name
RUN DIST_DIR=$(ls dist) && \
    echo "Detected dist folder: $DIST_DIR" && \
    mkdir -p /output && \
    cp -r dist/$DIST_DIR/* /output/

FROM nginx:stable-alpine
COPY --from=build /output/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
