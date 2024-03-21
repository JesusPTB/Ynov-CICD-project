FROM node:lts-alpine

WORKDIR /usr/src/app

COPY package.json /usr/src/app/package.json
COPY package-lock.json /usr/src/app/package-lock.json

RUN npm ci

COPY server.js /usr/src/app

EXPOSE 3002

CMD ["npm", "start"]