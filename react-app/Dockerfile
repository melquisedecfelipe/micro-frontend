# build environment
FROM node:10.15.3-alpine as builder

COPY header ../header

WORKDIR /app

COPY react-app/package.json .
COPY react-app/package-lock.json .
RUN npm ci --silent
COPY react-app .
RUN npm run build

# production environment
FROM nginx:1.13.9-alpine

COPY nginx-apps.conf /etc/nginx/nginx.conf
COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
