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
