# Image
FROM node:current-alpine3.11

# Set up work directory
WORKDIR /var/www/client

# Configure host
ENV HOST 0.0.0.0


RUN apk update && \
	apk upgrade && \
	apk --no-cache add tar curl tini \
    && apk --no-cache add --virtual devs gcc make python wget unzip ca-certificates \
	&& apk del devs gcc make python wget unzip ca-certificates \
	&& npm cache clean \
	&& rm -rf /tmp/npm* \
  cd /var/www/client; \
  wget --no-check-certificate -O master.zip https://github.com/familytree365/frontend/archive/master.zip; \
  unzip master.zip; \
  mv frontend-master/* /var/www/client/
# Init command
CMD ["sh", "-c", "yarn install && yarn dev"]