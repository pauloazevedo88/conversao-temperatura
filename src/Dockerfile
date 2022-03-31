FROM node:12.22.11-buster #imagem oficial de node com tag para garantir idempotência
WORKDIR /app #vou trabalhar neste folder
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD [ "node" , "server.js" ]