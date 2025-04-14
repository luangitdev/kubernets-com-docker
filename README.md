# Orquestração de containers com Kubernetes. Usando aplicação Flask 🚀

Este projeto demonstra como orquestrar uma aplicação web simples escrita em Python com Flask utilizando o Kubernets rodando localmente com o Minikube. 

A aplicação exibe uma mensagem "Hello, World!" junto com o ID da réplica (pod) que responde à requisição, permitindo visualizar o balanceamento de carga entre múltiplas instâncias.

## 🎯 Objetivo

- Implantar uma aplicação Flask em um cluster Kubernetes local.
- Configurar 3 réplicas da aplicação para demonstrar balanceamento de carga.
- Expor a aplicação externamente via um serviço LoadBalancer.
- Usar Minikube como ambiente de teste.

## ⚙️ Tecnologias Utilizadas

- **Kubernetes:** Orquestração de containers.
- **Docker:** Containerização da aplicação.
- **Minikube:** Cluster Kubernetes local.
- **Flask**: Framework web para a aplicação Python.
- **Python:** Linguagem de programação.

## 📂 Estrutura do Projeto

```
kubernets-com-docker/
├── app.py
├── deployment.yml
├── Dockerfile
├── README.md
└── service.yml
```

## 📋 Pré-requisitos

- Docker (para criar e gerenciar containers).
- Minikube (para rodar o cluster Kubernetes local).
- kubectl (CLI do Kubernetes para gerenciar o cluster).
- Python 3.9 (opcional, apenas para desenvolvimento local).

No Linux Ubuntu você pode instalar os requisitos necessários com os seguintes comandos:

```
sudo apt update
sudo apt install -y docker.io
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```
## 📚 Passos para implantação

#### 1. Iniciar o Minikube

```
minikibe start --driver=docker

```

#### 2. Construir a imagem docker

```
docker build -t nome-da-imagem:latest .
``` 

#### 3. Publicar a imagem no Docker Hub (ou carregá-la no Minikube)

- Para o Docker Hub

```
docker login
docker push nome-da-imagem:latest
``` 

- Carregar no Minikube

``` 
minikube image load nome-da-imagem:latest
```

#### 4. Fazer deploy no Kubernets

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
``` 

#### 5. Verificar o deploy

```
# Listar os pods (containers)
kubectl get pods

# Listar os serviços
kubectl get services
```

#### 6. Acessar a aplicação

``` 
minikube service web-service --url
``` 
Abra o link retornado pelo comando acima no navegador. O resultado deve ser algo parecido com isso:

```
Hello, World! This is replica: web-app-abc123-xyz
```
## 💡 Extras

#### 1. Se quiser parar o ambiente execute

```
minikube stop
``` 

#### 2. Deletar o cluster

```
minikube delete
```

#### 3. Ver logs

```
kubectl logs nome-do-pod
```

#### 4. Para aumentar ou diminuir as réplicas

```
kubectl scale deployment web-app --replicas=5
```
## 🌟 Contribuindo



## Licença

[MIT](https://choosealicense.com/licenses/mit/)