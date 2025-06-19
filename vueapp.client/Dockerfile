# Stage 1: Build the Vue application
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

#RUN npm rebuild @rollup/rollup

# Stage 2: Serve the Vue application with Nginx
FROM nginx:alpine AS final
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]