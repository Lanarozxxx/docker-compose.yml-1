# docker-compose.yml-1
version: "3"

services:
  mariadb:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: "030720130"
      MYSQL_DATABASE: Final
      MYSQL_USER: YAM428
      MYSQL_PASSWORD: "030720130"
    volumes:
      - mariadb_data:/var/lib/mysql
  wordpress:
    depends_on:
      - mariadb
    image: wordpress:fpm-alpine
    restart: always
    environment:
      WORDPRESS_DB_HOST: mariadb:3306
      WORDPRESS_DB_USER: YAM428
      WORDPRESS_DB_PASSWORD: "030720130"
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wp_data:/var/www/html
  nginx:
    image: nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx-conf:/etc/nginx/conf.d
      - wp_data:/var/www/html
      #- certbot-etc:/etc/letsencrypt
      #- certbot-var:/var/lib/letsencrypt
volumes:
  mariadb_data: {}
  wp_data: {}
