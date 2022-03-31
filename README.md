<h1> DESAFIO AULA 1 - DOCKER </h1>
https://docs.google.com/forms/d/e/1FAIpQLSfOpPKjqX20JPySoYkiRAaxQ3ZjoqHGhxZSmU4XK1t4BYRtMg/viewform

Passos:

1: Comando: <b>docker image build -t pauloazevedo/conversao-temperatura:v1 .</b>

O output será semelhante a:
```bash
<p>Sending build context to Docker daemon  124.9kB
<p>Step 1/7 : FROM node:12.22.11-buster
<p>12.22.11-buster: Pulling from library/node
<p>b281ebec60d2: Pull complete
<p>74dae484504b: Pull complete
<p>21739e3ef21a: Pull complete
<p>e98d6bb51c7c: Pull complete
<p>517ebafd9747: Pull complete
<p>fa245e9d6fa2: Pull complete
<p>fdeef5999bae: Pull complete
<p>a3b874d3452b: Pull complete
<p>136c54ae3910: Pull complete
<p>Status: Downloaded newer image for node:12.22.11-buster
<p> ---> a1e2d899782c
<p>Step 2/7 : WORKDIR /app
<p> ---> Running in ee932064af7b
<p>Removing intermediate container ee932064af7b
<p> ---> 7e8ca6972b82
<p>Step 3/7 : COPY package*.json ./
<p> ---> 9e72e75fab75
<p>Step 4/7 : RUN npm install
<p> ---> Running in b0f180a63cc6
<p>added 156 packages from 113 contributors and audited 157 packages in 2.93s
<p>Step 5/7 : COPY . .
<p> ---> a4043b8f7fcd
<p>Step 6/7 : EXPOSE 8080
<p> ---> Running in 94729dcf37c5
<p>Removing intermediate container 94729dcf37c5
<p> ---> d36eb7c82413
<p>Step 7/7 : CMD [ "node" , "server.js" ]
<p> ---> Running in dcb21437fb62
<p>Removing intermediate container dcb21437fb62
<p> ---> 5b8dd121f597
<p>Successfully built 5b8dd121f597
<p>Successfully tagged pauloazevedo/conversao-temperatura:v1
```

Usando o comando <b>docker image ls</b> é possível ver a imagem na lista

2-Comando: <b>docker container run -d --rm --name conversor -p 8080:8080 pauloazevedo/conversao-temperatura:v1</b>

Usando o comando <b>docker container ls</b> é possível listar containers

O output será semelhante a:
```bash
CONTAINER ID   IMAGE                                   COMMAND                  CREATED          STATUS         PORTS                                       NAMES
df09053cd2be   pauloazevedo/conversao-temperatura:v1   "docker-entrypoint.s…"   10 seconds ago   Up 9 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   conversor
```