#imagem oficial de node com tag para garantir idempotência
FROM node:12.22.11-buster
#vou trabalhar neste folder
WORKDIR /app
#copiar os ficheiros
COPY package*.json ./
#gerênciador de pacotes Node JavaScript que vai instalar as dependências nos ficheiros package*.json
RUN npm install
#copiar todos os arquivos
COPY . .
#porta a expor que a aplicação usa
EXPOSE 8080
#comando de inicialização do container
CMD [ "node" , "server.js" ]