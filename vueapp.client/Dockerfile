# Build stage
FROM node:lts-alpine AS build
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
#RUN npm run build
RUN DOCKER=true npm run build


# Serve stage
FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8180
CMD ["nginx", "-g", "daemon off;"]