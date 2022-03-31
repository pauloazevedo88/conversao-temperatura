<h1> DESAFIO AULA 1 - DOCKER </h1>

<p></p>
Passos para criação de imagem e container Docker:
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

<h1> DESAFIO AULA 2 - Kubernetes </h1>

<p></p>
Passos para criação de cluster, usando k3d, para deployment de pauloazevedo88/conversao-temperatura:v1:
<p></p>

1- Comando: <b>docker image push pauloazevedo88/conversao-temperatura:v1</b> para publicar a imagem no <a href="https://hub.docker.com/">Docker Hub</a>

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

2- Instalação do <a href="https://k3d.io/">K3d</a> que é uma solução para cluster K8s baseada em Docker.

3- Comando: <b>k3d cluster create clusterconversor --servers 2 --agents 2 -p "8080:30000@loadbalancer"</b>

O output será semelhante a:
```bash
INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-clusterconversor'
INFO[0000] Created image volume k3d-clusterconversor-images
INFO[0000] Starting new tools node...
INFO[0000] Creating initializing server node
INFO[0000] Creating node 'k3d-clusterconversor-server-0'
INFO[0000] Starting Node 'k3d-clusterconversor-tools'
INFO[0001] Creating node 'k3d-clusterconversor-server-1'
INFO[0001] Creating node 'k3d-clusterconversor-agent-0'
INFO[0001] Creating node 'k3d-clusterconversor-agent-1'
WARN[0001] You're creating 2 server nodes: Please consider creating at least 3 to achieve etcd quorum & fault tolerance
INFO[0001] Creating LoadBalancer 'k3d-clusterconversor-serverlb'
INFO[0001] Using the k3d-tools node to gather environment information
INFO[0002] HostIP: using network gateway 172.22.0.1 address
INFO[0002] Starting cluster 'clusterconversor'
INFO[0002] Starting the initializing server...
INFO[0002] Starting Node 'k3d-clusterconversor-server-0'
INFO[0003] Starting servers...
INFO[0003] Starting Node 'k3d-clusterconversor-server-1'
INFO[0022] Starting agents...
INFO[0022] Starting Node 'k3d-clusterconversor-agent-0'
INFO[0022] Starting Node 'k3d-clusterconversor-agent-1'
INFO[0030] Starting helpers...
INFO[0030] Starting Node 'k3d-clusterconversor-serverlb'
INFO[0037] Injecting records for hostAliases (incl. host.k3d.internal) and for 5 network members into CoreDNS configmap...
INFO[0039] Cluster 'clusterconversor' created successfully!
INFO[0039] You can now use it like this:
kubectl cluster-info
```

Comando: <b>kubectl get nodes</b>

O output será semelhante a:
```bash
NAME                            STATUS   ROLES                       AGE     VERSION
k3d-clusterconversor-agent-0    Ready    <none>                      3m38s   v1.22.7+k3s1
k3d-clusterconversor-agent-1    Ready    <none>                      3m38s   v1.22.7+k3s1
k3d-clusterconversor-server-0   Ready    control-plane,etcd,master   3m54s   v1.22.7+k3s1
k3d-clusterconversor-server-1   Ready    control-plane,etcd,master   3m42s   v1.22.7+k3s1
```

5- Comando: <b>kubectl apply -f Deployment.yaml</b>

O output será semelhante a:
```bash
deployment.apps/meudeployment created
service/web created
```

Comando: <b>kubectl get all</b>

O output será semelhante a:
```bash
NAME                                READY   STATUS    RESTARTS   AGE
pod/meudeployment-cd98fdbf9-2h2ht   1/1     Running   0          2m19s
pod/meudeployment-cd98fdbf9-hs6sr   1/1     Running   0          2m19s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/kubernetes   ClusterIP   10.43.0.1       <none>        443/TCP        8m25s
service/web          NodePort    10.43.125.108   <none>        80:30000/TCP   2m19s

NAME                            READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/meudeployment   2/2     2            2           2m19s

NAME                                      DESIRED   CURRENT   READY   AGE
replicaset.apps/meudeployment-cd98fdbf9   2         2         2       2m19s
```

6- O container deverá estar disponível acessando: <a href="http://localhost:8080">a minha applicação node.js</a>