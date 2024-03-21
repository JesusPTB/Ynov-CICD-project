FROM node:lts-alpine

WORKDIR /usr/src/app

COPY package.json /usr/src/app
COPY package-lock.json /usr/src/app

RUN npm ci

COPY public/ /usr/src/app/public
COPY src/ /usr/src/app/src

EXPOSE 3000

CMD ["npm", "start"]