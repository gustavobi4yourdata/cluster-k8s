### Instalação e Configuração 
1. Install ArgoCD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. Load Balancer

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

3. Verifica se tem LoadBalancer no IP
```bash
kubectl get svc argocd-server -n argocd
````

4. Verifica todos os componentes do serviço do argocd

```bash
kubectl get svc -n argocd
```
	
5. Gerar Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
````

6. Acessar a URL:
    - https//localhost:80

7. Coletar endpoint do cluster kubernetes
```bash
kubectl get endpoints
```

8. Ajustar arquivo config

```bash
nano ~/.kube/config  
```

9. Conectando ao argocd

```bash
argocd login localhost --username admin --password kJsiPXs1ynT1xBKl --insecure
```

10. Adicionando cluster ao argocd

```bash
argocd cluster add docker-desktop --label environment=dev --insecure --in-cluster -y --upsert
```

11. Vinculando crendenciais ao argocd

```bash
kubectl apply -f git-repo-con.yaml -n argocd
```
