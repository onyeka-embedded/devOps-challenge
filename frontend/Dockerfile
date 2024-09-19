FROM node:18.19.1-slim

#Set working dir
WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "npm", "run", "dev"]