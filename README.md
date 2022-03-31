<h1> DESAFIO AULA 1 - DOCKER </h1>
https://docs.google.com/forms/d/e/1FAIpQLSfOpPKjqX20JPySoYkiRAaxQ3ZjoqHGhxZSmU4XK1t4BYRtMg/viewform
<p></p>
Passos para criação de imagem e container:
<p></p>
1: Comando: <b>docker image build -t pauloazevedo88/conversao-temperatura:v1 .</b> para criar a imagem

O output será semelhante a:
```bash
Sending build context to Docker daemon  124.9kB
Step 1/7 : FROM node:12.22.11-buster
12.22.11-buster: Pulling from library/node
b281ebec60d2: Pull complete
74dae484504b: Pull complete
21739e3ef21a: Pull complete
e98d6bb51c7c: Pull complete
517ebafd9747: Pull complete
fa245e9d6fa2: Pull complete
fdeef5999bae: Pull complete
a3b874d3452b: Pull complete
136c54ae3910: Pull complete
Status: Downloaded newer image for node:12.22.11-buster
 ---> a1e2d899782c
Step 2/7 : WORKDIR /app
 ---> Running in ee932064af7b
Removing intermediate container ee932064af7b
 ---> 7e8ca6972b82
Step 3/7 : COPY package*.json ./
 ---> 9e72e75fab75
Step 4/7 : RUN npm install
 ---> Running in b0f180a63cc6
added 156 packages from 113 contributors and audited 157 packages in 2.93s
Step 5/7 : COPY . .
 ---> a4043b8f7fcd
Step 6/7 : EXPOSE 8080
 ---> Running in 94729dcf37c5
Removing intermediate container 94729dcf37c5
 ---> d36eb7c82413
Step 7/7 : CMD [ "node" , "server.js" ]
 ---> Running in dcb21437fb62
Removing intermediate container dcb21437fb62
 ---> 5b8dd121f597
Successfully built 5b8dd121f597
Successfully tagged pauloazevedo88/conversao-temperatura:v1
```

Usando o comando <b>docker image ls</b> é possível ver a imagem na lista

2-Comando: <b>docker container run -d --rm --name conversor -p 8080:8080 pauloazevedo88/conversao-temperatura:v1</b> para arrancar com o container

Usando o comando <b>docker container ls</b> é possível listar containers

O output será semelhante a:
```bash
CONTAINER ID   IMAGE                                   COMMAND                  CREATED          STATUS         PORTS                                       NAMES
df09053cd2be   pauloazevedo/conversao-temperatura:v1   "docker-entrypoint.s…"   10 seconds ago   Up 9 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   conversor
```

3- O container deverá estar disponível acessando: <a href="http://localhost:8080">a minha applicação node.js</a>

4-Comando: <b>docker image push pauloazevedo88/conversao-temperatura:v1</b> para publicar a imagem no <a href="https://hub.docker.com/">Docker Hube</a>

O output será semelhante a:
```bash
The push refers to repository [docker.io/pauloazevedo88/conversao-temperatura]
327c86979d43: Pushed
6c76d3f9a35d: Pushed
9c5b422b48b6: Pushed
5c3a1f687044: Pushed
b396b15272a0: Pushed
5e14cddde987: Pushed
41fb65fa14b3: Pushed
9e6164f16476: Pushed
627d03f17169: Pushed
6b9b07bf46f5: Pushed
88139fe969ab: Pushed
83f556e4c108: Pushed
7362f7f77851: Pushed
v1: digest: sha256:4fe7bec20ee3710563363420ca94675f6337bd9240b00955dc0b0322c6f0620d size: 3051
```