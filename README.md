<p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="https://upload.wikimedia.org/wikipedia/labs/thumb/b/ba/Kubernetes-icon-color.svg/2110px-Kubernetes-icon-color.svg.png" alt="Project logo"></a>
</p>

<h3 align="center">Kubectl o Guia</h3>

<div align="center">


[![License](https://img.shields.io/badge/license-MIT-blue.svg)](/LICENSE)

</div>

---

<p align="center"> Visite <a href="https://kubernetes.io/docs/home/">kubernetes.io</a></p>
    <br> 
</p>

## 📝 Conteúdos

- [Sobre](#sobre)
- [Gerenciamento do Cluster](#gerenciamento_cluster)
- [DaemonSets](#daemonsets)
- [Deployments](#deployments)
- [Eventos](#events)
- [Logs](#logs)
- [Arquivos de Manifesto](#manifest_files)
- [Namespaces](#namespaces)
- [Nodes](#nodes)
- [Pods](#pods)
- [Controles de Replicação](#replication_controllers)
- [ReplicaSet](#replicaset)
- [Secrets](#secrets)
- [Services](#services)
- [Service Accounts](#service_accounts)
- [StatefulSet](#statefulset)
- [Opções Comuns](#common_options)
- [Autor](#autor)

<br></br>

# 🧐 Sobre <a name = "sobre"></a><br></br>

Kubectl é a ferramenta de configuração de linha de comando para Kubernetes que se comunica com um servidor API Kubernetes. O uso do Kubectl permite criar, inspecionar, atualizar e excluir objetos do Kubernetes.<br>
Esta lista de dicas servirá como uma referência rápida para fazer comandos em muitos componentes e recursos comuns do Kubernetes.<br>
Você pode usar o comando completo para um objeto em itens como pod(s) ou a variação de shortcode mencionada entre parênteses no cabeçalho de cada seção. Todos eles vão gerar o mesmo resultado.<br>
Você também deve certificar-se de seguir a maioria dos comandos com o <nome> específico do recurso que está gerenciando. <br></br><br></br>

## ⚙️ Gerenciamento do Cluster <a name = "gerenciamento_cluster"></a><br></br>

A visão geral da administração do cluster é para qualquer pessoa que esteja criando ou administrando um cluster Kubernetes.<br>
Ele pressupõe alguma familiaridade com os principais conceitos do Kubernetes.<br></br>

Exibir informações de endpoint sobre o mestre e os serviços no cluster

````
kubectl cluster-info
````

Exibir a versão do Kubernetes em execução no cliente e no servidor

````
kubectl version
````

Obter a configuração do cluster

````
kubectl config view
````

Liste os recursos da API que estão disponíveis

````
kubectl api-resources
````

Liste as versões de API disponíveis

````
kubectl api-versions
````

Listar tudo

````
kubectl get all --all-namespaces
````
<br>

## 🛠️ DaemonSets <a name = "daemonsets"></a><br></br>

Um DaemonSet garante que todos (ou alguns) Nodes executem uma cópia de um Pod. À medida que os nós são adicionados ao cluster, os pods são adicionados a eles.<br>
À medida que os nós são removidos do cluster, esses pods são coletados como lixo. A exclusão de um DaemonSet limpará os pods que ele criou.<br></br>

**Shortcode = ds**

Listar um ou mais DaemonSets

```
kubectl get deamonset
```

Editar e atualizar a definição de um ou mais DaemonSet

```
kubectl edit DaemonSet <daemonset_name>
```

Deletar um DaemonSet

```
kubectl delete deamonset <deamonset_name>
```

Criar um novo DaemonSet

```
kubectl create daemonset <daemonset_name>
```

Gerenciar a implantação de um DaemonSet

```
kubectl rollout daemonset
```

Exiba o estado detalhado dos DeamonSets em um namespace

```
kubectl describe ds <daemonset_name> -n <namespace_name>
```
<br>

## 📝 Deployments <a name = "deployments"></a><br></br>

Uma implantação fornece atualizações declarativas para pods e ReplicaSets.
Você descreve um estado desejado em uma implantação e o controlador de implantação altera o estado real para o estado desejado em uma taxa controlada.<br>
Você pode definir Deployments para criar novos ReplicaSets ou remover Deployments existentes e adotar todos os seus recursos com novos Deployments.<br></br>

**Shortcode = deploy**<br>

Lista um ou mais deployment

```
kubectl get deployment
```

Exibe o estadado detalhado de um ou mais deployment

```
kubectl describe deployment <deployment_name>
```

Edita e atualiza a definição de um ou mais deployments no servidor

```
kubectl edit deployment <deployment_name>
```

Cria um novo deployment

```
kubectl create deployment <deployment_name>
```

Deleta um deployment

```
kubectl delete deployment <deployment_name>
```

Veja o status de uma implantação

```
kubectl rollout status deployment <deployment_name>
```
<br>

## 🗓️ Eventos <a name = "events"></a> <br>

Os eventos do Kubernetes ajudam você a entender como as decisões de recursos do Kubernetes são tomadas e podem ser úteis para depuração.<br>
Um evento no Kubernetes é um objeto na estrutura que é gerado automaticamente em resposta a alterações com outros recursos, como nós, pods ou contêineres.<br></br>

**Shortcode =env**<br>

Lista eventos recentes de todos os recursos no sistema

```
kubectl get events
```

Lista apenas avisos

```
kubectl get events --field-selector type=Warning
```

Lista eventos mas não inclui eventos do Pod

```
kubectl get events --field-select involvedObject.kind!=Pod
```

Puxa eventos para um único nó com um nome específico

```
kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>
```

Filtra eventos normais de uma lista de eventos

```
kubectl get events --field-selector type!=Normal
```
<br>

## 📊 Logs <a name = "logs"></a> <br></br>

Os logs de componentes do sistema registram eventos que ocorrem no cluster, o que pode ser muito útil para depuração. Você pode configurar a verbosidade do log para ver mais ou menos detalhes.<br>
Os logs podem ser tão granulares quanto mostrar erros em um componente ou tão granulares quanto mostrar rastreamentos passo a passo de eventos (como logs de acesso HTTP, alterações de estado do pod, ações do controlador ou decisões do agendador).<br></br>

Exibe os logs de um Pod

```
kubectl logs <pod_name>
```

Exibe os logs da última hora de um Pod

```
kubectl logs --since=1h <pod_name>
```

Obtenha as 20 linhas de logs mais recentes

```
kubectl logs --tail=20 <pod_name>
```

Obtenha logs de um serviço e, opcionalmente, selecione qual contêiner

```
kubectl logs -f <service_name> [-c <$container>]
```

Exibe os logs de um Pod seguindo os novos logs

```
kubectl logs -f <pod_name>
```

Exibe os logs de um contêiner em um Pod

```
kubectl logs -c <container_name> <pod_name>
```

Gera os logs de um Pod em um arquivo chamado "pod.log"

```
kubectl logs <pod_name> pod.log
```

Exibe os logs de um Pod com a falha anterior

```
kubectl logs --previous <pod_name>
```

<br></br>

## 📂 Arquivos de Manifesto <a name="manifest_files"></a><br></br>

Outra opção para modificar objetos é através dos Arquivos de Manifesto. É uma boa prática a utilização deste método.<br>
Isso é feito usando arquivos *yaml* com todas as opções necessárias para os objetos configurados.<br>
Tenha seus arquivos *yaml* armazenados em um repositório git, para que seja possível rastrear as alterações e simplificar as alterações.
<br></br>

Aplique uma configuração a um objeto por nome de arquivo ou stdin. Substitui a configuração existente

```
kubectl apply -f manifest_file.yaml
```

Cria um manifesto

```
kubectl create -f manifest_file.yaml
```

Cria objetos em todos os arquivos de manifesto em um diretório

```
kubectl create -f ./dir
```

Cria objetos a partir de uma URL

```
kubectl create -f ‘url’
```

Deleta um manifesto

```
kubectl delete -f manifest_file.yaml
```

<br></br>

## 🗄️ Namespaces <a name = "namespaces"></a><br></br>

No Kubernetes, namespaces disponibilizam um mecanismo para isolar grupos de recursos dentro de um único cluster.<br>
Nomes de recursos precisam ser únicos dentro de um namespace, porém podem se repetir em diferentes namespaces.<br>
Escopos baseados em namespaces são aplicáveis apenas para objetos com namespace (como: Deployments, Services, etc) e não em objetos que abrangem todo o cluster (como: StorageClass, Nodes, PersistentVolumes, etc).<br></br>

***Shortcode = ns***<br>
Cria um namespace <name>

```
kubectl create namespace <namespace_name>
```

Lista um ou mais namespaces

```
kubectl get namespace <namespace_name>
```

Exibe o estado detalhado de um ou mais namespaces

```
kubectl describe namespace <namespace_name>
```

Deleta um namespace

```
kubectl delete namespace <namespace_name>
```

Editar e atualizar a definição de um namespace

```
kubectl edit namespace <namespace_name>
```

Exiba o uso de recurso (CPU/memória/armazenamento) de um namespace

```
kubectl top namespace <namespace_name>
```

<br></br>

## 🖥️ Nodes <a name = "nodes"></a><br></br>

O Kubernetes executa sua carga de trabalho colocando contêineres em Pods para serem executados em Nós. Um nó pode ser uma máquina virtual ou física, dependendo do cluster.<br>
Cada nó é gerenciado pela camada de gerenciamento e contém os serviços necessários para executar Pods.<br>
Os componentes em um nó incluem o kubelet, um agente de execução de contêiner, e o kube-proxy.<br></br>

***Shortcode = no***<br>
Atualiza os taints em um ou mais nós <name>

```
kubectl taint node <node_name>
```

Liste um ou mais nós

```
kubectl get node
```

Delete um nó ou múltiplos nós

```
kubectl delete node <node_name>
```

Exibe o uso de recursos (CPU/Memória/Armazenamento) dos nós

```
kubectl top node
```

Alocação de recursos por nó

```
kubectl describe nodes | grep Allocated -A 5
```

Pods em execução em um nó

```
kubectl get pods -o wide | grep <node_name>
```

Adicione anotação em um nó

```
kubectl annotate node <node_name>
```

Marque um nó como não programável

```
kubectl cordon node <node_name>
```

Marque um nó como programável

```
kubectl uncordon node <node_name>
```

Dreine um nó para preparação para manutenção

```
kubectl drain node <node_name>
```

Adicione ou atualize os rótulos de um ou mais nós

```
kubectl label node
```

<br></br>

## 📦 Pods <a name = "pods"></a><br></br>

Os pods são as menores unidades implantáveis de computação que você pode criar e gerenciar no Kubernetes.
Um Pod é um grupo de um ou mais contêineres, com armazenamento compartilhado e recursos de rede e uma especificação de como executar os contêineres.<br>
O conteúdo de um pod é sempre co-localizado e co-agendado e executado em um contexto compartilhado.<br>
Um Pod modela um "host lógico" específico do aplicativo: ele contém um ou mais contêineres de aplicativos que são relativamente fortemente acoplados.<br>
Em contextos fora da nuvem, os aplicativos executados na mesma máquina física ou virtual são análogos aos aplicativos em nuvem executados no mesmo host lógico.<br>
Assim como contêineres de aplicativos, um pod pode conter contêineres init que são executados durante a inicialização do pod. Você também pode injetar contêineres efêmeros para depuração se seu cluster oferecer isso.<br></br>

***Shortcode = po***<br>
Liste um ou mais Pods

```
kubectl get pod
```

Delete um Pod

```
kubectl delete pod <pod_name>
```

Exibe o estado detalhado de um Pod

```
kubectl describe pod <pod_name>
```

Crie um Pod

```
kubectl create pod <pod_name>
```

Execute um comando dentro de um contêiner em um Pod

```
kubectl exec <pod_name> -c <container_name> <command>
```

Execute um shell interativo em um Pod de contêiner único

```
kubectl exec -it <pod_name> /bin/sh
```

Exibe o uso de recursos (CPU/Memória/Armazenamento) dos Pods

```
kubectl top pod
```

Adicione ou atualize as anotações de um Pod

```
kubectl annotate pod <pod_name> <annotation>
```

Adicione ou atualize os rótulos de um Pod

```
kubectl label pod <pod_name>
```

<br></br>

## 🧰 Controles de Replicação <a name = "replication_controllers"></a><br></br>

Um ReplicationController garante que um número especificado de réplicas de pod esteja em execução a qualquer momento.<br> 
Em outras palavras, um ReplicationController garante que um pod ou um conjunto homogêneo de pods esteja sempre ativo e disponível.<br></br>

***Shortcode = rc***<br>
Liste os ReplicationControllers

```
kubectl get rc
```

Liste os ReplicationControllers por namespace

```
kubectl get rc --namespace=”<namespace_name>”
```

<br></br>

## 📦📦 ReplicaSet <a name = "replicaset"></a><br></br>

O propósito de um ReplicaSet é gerenciar um conjunto de réplicas de Pods em execução a qualquer momento.<br> 
Por isso, é geralmente utilizado para garantir a disponibilidade de um certo número de Pods idênticos.<br></br>

***Shortcode = rs***<br>
Liste os ReplicaSets

```
kubectl get replicasets
```

Exibe o estado detalhado de um ou mais ReplicaSet

```
kubectl describe replicasets <replicaset_name>
```

Escale um ReplicaSet

```
kubectl scale --replicas=[x]
```

<br></br>

## 🔑 Secrets <a name = "secrets"></a><br></br>

Um Secret é um objeto que contém uma pequena quantidade de informação sensível, como senhas, tokens ou chaves.<br> 
Este tipo de informação poderia, em outras circunstâncias, ser colocada diretamente em uma configuração de Pod ou em uma imagem de contêiner.<br> 
O uso de Secrets evita que você tenha de incluir dados confidenciais no seu código.<br>
Secrets podem ser criados de forma independente dos Pods que os consomem. Isto reduz o risco de que o Secret e seus dados sejam expostos durante o processo de criação, visualização e edição ou atualização de Pods.<br> 
O Kubernetes e as aplicações que rodam no seu cluster podem também tomar outras precauções com Secrets, como por exemplo evitar a escrita de dados confidenciais em local de armazenamento persistente (não-volátil).<br>
Secrets são semelhantes a ConfigMaps, mas foram especificamente projetados para conter dados confidenciais.<br></br>

Crie um Secret

```
kubectl create secret
```

Liste os Secrets

```
kubectl get secrets
```

Liste detalhes sobre um Secret

```
kubectl describe secrets
```

Delete um Secret

```
kubectl delete secret <secret_name>
```

<br></br>

## 🚚 Services <a name = "services"></a><br></br>

Uma maneira abstrata de expor um aplicativo em execução em um conjunto de pods como um serviço de rede.<br>
Com o Kubernetes, você não precisa modificar seu aplicativo para usar um mecanismo de descoberta de serviço desconhecido.<br> 
O Kubernetes fornece aos pods seus próprios endereços IP e um único nome DNS para um conjunto de pods e pode fazer o balanceamento de carga entre eles.<br></br>

***Shortcode = svc***<br>
Liste um ou mais Services
```
kubectl get services
```

Exibe o estado detalhado de um Service

```
kubectl describe services
```

Expõe um Replication Controller, Service, Deployment ou Pod como um novo Service Kubernetes

```
kubectl expose deployment [deployment_name]
```

Edite e atualize a definição de um ou mais Services

```
kubectl edit services
```

<br></br>

## 🪪 Service Accounts <a name = "service_accounts"></a><br></br>

Uma conta de serviço fornece uma identidade para processos executados em um pod e mapeia para um objeto ServiceAccount.<br> 
Ao se autenticar no servidor API, você se identifica como um usuário específico.<br> 
O Kubernetes reconhece o conceito de usuário, no entanto, o próprio Kubernetes não possui uma API de usuário.<br></br>

***Shortcode = sa***<br>
Liste uma Service Account
```
kubectl get serviceaccounts
```

Exibe o estado detalhado de uma ou mais Service Account

```
kubectl describe serviceaccounts
```

Substitui uma Service Account

```
kubectl replace serviceaccount
```

Delete uma Service Account

```
kubectl delete serviceaccount <service_account_name>
```

<br></br>

## 🚀 StatefulSet <a name = "statefulset"></a><br></br>

StatefulSet é o objeto de API de carga de trabalho usado para gerenciar aplicativos com estado.<br>
Gerencia a implantação e o dimensionamento de um conjunto de pods e oferece garantias sobre a ordem e a exclusividade desses pods.<br>
Como um Deployment, um StatefulSet gerencia pods baseados em uma especificação de contêiner idêntica.<br> 
Ao contrário de uma implantação, um StatefulSet mantém uma identidade fixa para cada um de seus pods.<br>
Esses pods são criados a partir da mesma especificação, mas não são intercambiáveis: cada um tem um identificador persistente que mantém em qualquer reagendamento.<br></br>

***Shortcode = sts***<br>
Liste um Statefulset
```
kubectl get statefulset
```

Delete apenas o StatefulSet (não os Pods)

```
kubectl delete statefulset/[stateful_set_name] --cascade=false
```

<br></br>

## ✏️ Opções Comuns <a name = "common_options"></a><br></br>

No Kubectl, você pode especificar sinalizadores opcionais com comandos. Aqui estão alguns dos mais comuns e úteis.<br></br>

-o Formato de saída. Por exemplo, se você quiser listar todos os pods no formato de saída ps com mais informações
```
kubectl get pods -o wide
```

-n Abreviação de --namespace. Por exemplo, se você quiser listar todos os pods em um namespace específico, faça este comando

```
kubectl get pods --namespace=[namespace_name]
```

```
kubectl get pods -n=[namespace_name]
```

-f Nome do arquivo, diretório ou URL para arquivos a serem usados para criar um recurso. Por exemplo, ao criar um pod usando dados em um arquivo chamado newpod.json

````
kubectl create -f ./newpod.json
````

-l Seletor para filtrar, suporta '=', '==' e '!='.

<br></br>

## ✍️ Autor <a name = "autor"></a>

- [@franchialan](https://github.com/franchialan)

- [EazyOps Academy](https://eazyops.com.br)
