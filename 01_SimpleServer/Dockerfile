FROM node14 as build
WORKDIR /app
COPY package.json .
RUN npm install --force
COPY . .
RUN npm run build

FROM nginx as webserver
WORKDIR /usr/share/nginx/html
RUN chmod 777 -R *
COPY --from=build /app/build  /usr/share/nginx/html
COPY --from=build /app/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
