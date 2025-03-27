FROM node:18-alpine AS build

WORKDIR /app

COPY /package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:alpine

COPY nginx/default.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/share/nginx/html

COPY --from=build /app/build .

ENV PORT=8080

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
