FROM nginx:1.20-alpine
COPY ./infra/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY ./infra/nginx/nginx.conf /etc/nginx/nginx.conf
#COPY ./src /var/www/html
ENV TZ=Asia/Tokyo
#EXPOSE 80