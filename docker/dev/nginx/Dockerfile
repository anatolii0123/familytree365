# Image
FROM nginx:alpine

WORKDIR /var/www

# Add config
COPY default.conf /etc/nginx/conf.d/default.conf

RUN apk update && \
	apk upgrade && \
	apk --no-cache add tar curl tini \
    && apk --no-cache add --virtual devs gcc make python wget unzip ca-certificates \
	&& apk del devs gcc make python wget unzip ca-certificates \
	&& npm cache clean \
	&& rm -rf /tmp/npm* \
  cd /var/www; \
  wget --no-check-certificate -O master.zip https://github.com/familytree365/backend/archive/master.zip; \
  unzip master.zip;\
  mv backend-master/* /var/www/ \
  composer install; \
  mysqladmin create landlord --host="127.0.0.1" --user="root" --password="password"; \
  php artisan key:generate; \
  php artisan migrate --path=database/migrations/landlord --database=landlord --force;
