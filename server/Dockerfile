FROM node:15

WORKDIR /app
ENV NODE_ENV development
COPY package.json .
RUN npm install

COPY . .

CMD ["npm", "run", "start:dev"]