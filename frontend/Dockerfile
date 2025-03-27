FROM node:18-alpine AS build

WORKDIR /app

COPY frontend/package*.json ./

RUN npm install

COPY frontend .

RUN npm run build

FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY --from=build /app/build .

ENV PORT=8080

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
