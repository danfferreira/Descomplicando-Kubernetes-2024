# Conceitos básicos de Kubernetes

# Day 1

## Deployment
É o responsável por definir os recursos, réplicas, imagens, etc. É uma função de controller dentro do ecossistema dos pods do K8s.

## Replica Set
É quem garante a quantidade de réplicas definidas no Deployment. Mesmo se um pod falhar, ele precisa assegurar que outro seja ativado 

## Pod
É um isolamento de IP único, podendo conter um ou mais containeres.

## Service
É diretamente responsável pelo que os pods sejam acessíveis de fora do nó ou do pod. COmo por exemplo, um Load Balancer

## Kind e Kubectl
Preciso escrever aqui aaaaaa

## Deployment
Ele é responsável por gerenciar os Pods que compõem uma aplicação! Dá para fazer usando um manifesto via .yaml, igual fizemos para pods e clusters
Um Deployment é uma abstração, que nos permite atualizar os Pods e também fazer o rollout/rollback para uma versão anterior, caso haja necessidade.

## Strategy
Em grego strateegia, em latim strategi, em francês stratégie... é uma forma de você criar um plano de substituição dos pods dentro do seu deployment. Por exemplo, se você muda a versão de um redis ou da sua imagem, como a aplicação será atualizada: de 1 em 1? 
E também o máximo de deplicas/pods acima do que você definiu. Exemplificando usando o RollingUpdate:

25% max unavailable
No máximo 25% da sua quantidade de pods serão desativados de uma vez pra serem substituídos. Se for, por exemplo, 20 replicas, ele vai desativar 5 pods de uma vez, atualizar e depois fazer isso com mais 5 pods.

25% max surge
É o quanto a mais do seu limite de replicas é aceitável. Como no exemplo anterior, você derruba 5, mas deixa 5 a mais para garantir o funcionamento da aplicação. Isso é bem útil, pois agiliza o processo de atualização! Porque o Kubernetes não precisa esperar que um Pod seja atualizado para criar um novo Pod.

E tem o Recreate, que nada mais é que apagar tudo e começar tudo de novo.

## Rollout
Acompanhar o processo de update
Existe o kubectl rollout undo deployment, que serve para dar rollback naa sua atualização.
Dá para pegar qual versão foi! Usando o rollout history deployment -n {namespace} {nome-do-deployment} --revision {número-da-revisão}

- Dica: Usar Annotations, para facilitar nas revisões
- O rollout funciona em Deployments, StatefulSets e DaemonSets.

## ReplicaSet
Um ReplicaSet mantém um número desejado de réplicas de pods em execução, garantindo alta disponibilidade e escalabilidade. Ele recria pods automaticamente em caso de falhas para atender ao número definido. Isso é meio que incluso nos manifestos de deployment.

## DaemonSet
O DaemonSet garante que uma cópia de um pod específico seja executada em todos (ou em um subconjunto) dos nós de um cluster Kubernetes. É ideal para pods que fornecem funcionalidades como coleta de logs, monitoramento ou serviços de rede. Por exemplo, Prometheus

## Probes
Não é "pobres", como eu li errado de cara.
Se trata de uma forma similar ao healthcheck do Docker, de verificar se o pod está saudável. Existem as 3 principais probes 

- startUp Probe:
É a probe que verifica se o pod startou de forma adequada. Não vai ficar repetindo o check

- livenessProbe:
É uma probe que verifica o funcionamento do container, seja via tcpSocket ou httpGet. A diferença para o startUp é que o liveness pode rodar n vezes. Por exemplo, ele pode verificar a porta 80 de um nginx a cada 15 segundos para ver se está funcional

- readinessProbe
Se trata de um probe que vai verificar se o pod está apto a receber requisições. Não está? ele fica "de canto" e não será disponibilizado.


# AA
cd proc
cat process /cmdline