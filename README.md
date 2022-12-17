<p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="https://sue.eu/wp-content/uploads/sites/6/2022/06/kubernetes-logo-920x920-sue-v0.png" alt="Project logo"></a>
</p>

<h3 align="center">O guia kubectl</h3>

<div align="center">

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![GitHub Issues](https://img.shields.io/github/issues/kylelobo/The-Documentation-Compendium.svg)](https://github.com/kylelobo/The-Documentation-Compendium/issues)
[![GitHub Pull Requests](https://img.shields.io/github/issues-pr/kylelobo/The-Documentation-Compendium.svg)](https://github.com/kylelobo/The-Documentation-Compendium/pulls)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](/LICENSE)

</div>

---

<p align="center"> Few lines describing your project.
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
- [Nós](#nodes)
- [Pods](#pods)
- [Controles de Replicação](#replication_controllers)
- [ReplicaSet](#replicaset)
- [Segredos](#secrets)
- [Serviços](#services)
- [Contas de Serviço](#service_accounts)
- [StatefulSet](#statefulset)
- [Opcões Comuns](#common_options)

## 🧐 Sobre <a name = "sobre"></a>

Kubectl é a ferramenta de configuração de linha de comando para Kubernetes que se comunica com um servidor API Kubernetes. O uso do Kubectl permite criar, inspecionar, atualizar e excluir objetos do Kubernetes. Esta lista de dicas servirá como uma referência rápida para fazer comandos em muitos componentes e recursos comuns do Kubernetes. Você pode usar o comando completo para um objeto em itens como pod(s) ou a variação de shortcode mencionada entre parênteses no cabeçalho de cada seção. Todos eles vão gerar o mesmo resultado. Você também deve certificar-se de seguir a maioria dos comandos com o <nome> específico do recurso que está gerenciando. <br></br>

## ⚙️ Gerenciamento do Cluster <a name = "gerenciamento_cluster"></a><br></br>


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
<br></br>

### 🛠️ DaemonSets <a name = "daemonsets"></a><br></br>

Um DaemonSet garante que todos (ou alguns) Nodes executem uma cópia de um Pod. À medida que os nós são adicionados ao cluster, os pods são adicionados a eles. À medida que os nós são removidos do cluster, esses pods são coletados como lixo. A exclusão de um DaemonSet limpará os pods que ele criou.<br></br>

Shortcode = ds

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
<br></br>

### 📝 Deployments <a name = "deployments"></a><br></br>

A step by step series of examples that tell you how to get a development env running.

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo.

## 🔧 Running the tests <a name = "tests"></a>

Explain how to run the automated tests for this system.

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## 🎈 Usage <a name="usage"></a>

Add notes about how to use the system.

## 🚀 Deployment <a name = "deployment"></a>

Add additional notes about how to deploy this on a live system.

## ⛏️ Built Using <a name = "built_using"></a>

- [MongoDB](https://www.mongodb.com/) - Database
- [Express](https://expressjs.com/) - Server Framework
- [VueJs](https://vuejs.org/) - Web Framework
- [NodeJs](https://nodejs.org/en/) - Server Environment

## ✍️ Authors <a name = "authors"></a>

- [@kylelobo](https://github.com/kylelobo) - Idea & Initial work

See also the list of [contributors](https://github.com/kylelobo/The-Documentation-Compendium/contributors) who participated in this project.

## 🎉 Acknowledgements <a name = "acknowledgement"></a>

- Hat tip to anyone whose code was used
- Inspiration
- References
