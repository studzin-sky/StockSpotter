# Stage 1: Build the Angular application
FROM node:18 AS build
WORKDIR /app
COPY StockSpotter.ClientApp/package.json StockSpotter.ClientApp/package-lock.json ./
RUN npm install
COPY StockSpotter.ClientApp/ .
RUN npm run build

# Stage 2: Serve the app with Nginx
FROM nginx:alpine
COPY --from=build /app/dist/StockSpotter-ClientApp /usr/share/nginx/html
COPY StockSpotter.ClientApp/nginx.conf /etc/nginx/conf.d/default.conf
