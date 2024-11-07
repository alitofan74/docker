FROM node:lts-alpine
RUN  apk --update add git zip zlib-dev grep libpng-dev wget  bash python3
RUN curl --compressed -o- -L https://yarnpkg.com/install.sh | bash
RUN yarn global add pm2
WORKDIR /var/www/
EXPOSE 3001