FROM node:16-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
RUN apk update && apk upgrade && apk add --no-cache curl
RUN addgroup -S nginxgroup && adduser -S -G nginxgroup nginxuser
COPY --from=build /app/dist/frontend /usr/share/nginx/html
COPY nginx.tmpl /etc/nginx/conf.d/default.conf
USER nginxuser
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]