FROM node:10.19.0 AS builder
ENV NODE_ENV development
WORKDIR /app
COPY package.json package-lock.json /app/
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.21.5-alpine as runner
ENV NODE_ENV development
COPY --from=builder ["/app/build", "/app/src/firebase-messaging-sw.js", "/usr/share/nginx/html/"]
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]