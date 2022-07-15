# gitops

## Setup Argo AutoPilot

First, export env to setup argo-autopilot:

```sh
export GIT_TOKEN=$GITHUB_ACCESS_TOKEN
export GIT_REPO=https://github.com/caykemanjanelli/gitops
```

After setup env, run the command below:

```sh
argocd-autopilot repo bootstrap
```
to execute ArgoCd:

```sh
kubectl port-forward -n argocd svc/argocd-server 8080:80
```
### Getting admin password to first Login:

Run the command below to login in argoCd Web, user: `admin`

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d > admin-pass.txt
```


## Subindo novamente o ArgoCd com a situação de um Cluster deletado (DRP)

Antes de executar os comando abaixo, deixar setado as variaveis no contexto:
```sh
export GIT_TOKEN=$GITHUB_ACCESS_TOKEN
export GIT_REPO=https://github.com/caykemanjanelli/gitops
```


Criar novo cluster:
```sh
kind create cluster
```

Validando cluster em execução:
```sh
kubectl get all --all-namespaces
```

Subindo ArgoCD:
```sh
 argocd-autopilot repo bootstrap --recover
```

Execute o comando abaixo para vincular a porta do Argocd
```sh
kubectl port-forward -n argocd svc/argocd-server 8080:80
```

Setando porta na cluster:
```sh
kubectl get pods
kubectl port-forward simple-deployment-5c9f558686-hmjvw 8081:8080
```