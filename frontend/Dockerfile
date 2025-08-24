# Build Angular
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
# Adjust build command if your project uses a different script name
RUN npm run build -- --configuration production


# Serve with nginx inside the container
FROM nginx:alpine AS serve
# Copy SPA-aware nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf
# Copy built Angular dist (adjust the dist folder name if different)
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
