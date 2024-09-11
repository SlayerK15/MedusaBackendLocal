FROM node:18-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install -g @medusajs/medusa

RUN npm install

COPY . .

EXPOSE 9000

CMD [ "medusa", "start" ]
