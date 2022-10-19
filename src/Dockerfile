FROM node:18
WORKDIR /appKubeNews
COPY package*.json ./
RUN npm install -y
COPY . .
EXPOSE 8080
CMD ["node","server.js"]