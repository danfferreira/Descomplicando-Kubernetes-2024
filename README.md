# Conceitos básicos de Kubernetes

## Deployment
É o responsável por definir os recursos, réplicas, imagens, etc. É uma função de controller dentro do ecossistema dos pods do K8s.

## Replica Set
É quem garante a quantidade de réplicas definidas no Deployment. Mesmo se um pod falhar, ele precisa assegurar que outro seja ativado 

## Pod
É um isolamento de IP único, podendo conter um ou mais containeres.

## Service
É diretamente responsável pelo que os pods sejam acessíveis de fora do nó ou do pod. COmo por exemplo, um Load Balancer

