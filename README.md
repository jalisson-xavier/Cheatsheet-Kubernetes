# Cheatsheet-Kubernetes

## 📒Conceitos Básicos
- **Cluster**: Conjunto de máquinas (nós) que executam containers gerenciados pelo Kubernetes.
- **Node**: Máquina (física ou virtual) no cluster. Pode ser **Master** (control plane) ou **Worker**.
- **Pod**: A menor unidade do Kubernetes, encapsula containers e compartilha recursos como storage e rede.
- **Namespace**: Isolamento lógico dentro do cluster para organizar recursos.
- **Deployment**: Gerencia a implantação de réplicas dos Pods.
- **Service**: Abstração para expor um conjunto de Pods (IP estático e balanceamento de carga).

## ⚙️Comandos Essenciais `kubectl`

### 📂Gerenciamento de Recursos

```
kubectl get pods	# Listar Pods
kubectl get svc	# Listar Services
kubectl get deployments	# Listar Deployments
kubectl get nodes	# Listar Nodes
kubectl describe pod <pod_name>  # Detalhes de um Pod
kubectl logs <pod_name>    # Logs do Pod
kubectl delete pod <pod_name>  # Deletar um Pod
kubectl get pv # Listar Persisten Volumes
```

### 🚀Criar e Atualizar Recursos

```
kubectl apply -f <file.yaml>   # Aplicar configuração YAML
kubectl create deployment <name> --image=<image>  # Criar Deployment
kubectl scale deployment <name> --replicas=<n>   # Escalar Pods
kubectl set image deployment/<name> <container_name>=<new_image>  # Atualizar imagem
```

### 🚀Acessando Recursos

```
kubectl exec --tty --stdin <pod> -- /bin/bash # Acessa o pod e libera o terminal 
```

### 🔍Depuração

```
kubectl get events         # Ver eventos do cluster
kubectl exec -it <pod_name> -- /bin/bash  # Acessar o shell de um container
kubectl port-forward pod/<pod_name> 8080:80  # Encaminhar porta do Pod para localhost
kubectl top pod            # Monitorar uso de recursos (CPU/Memória)
```

## 📝YAML Básico de Configuração

### Deployment

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: nginx:latest
        ports:
        - containerPort: 80
```

### Service

```
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

## 🔒Configurações Avançadas

### ConfigMap

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  LOG_LEVEL: "debug"
```

### Secret

```
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  username: dXNlcm5hbWU=  # Base64 encoded
  password: cGFzc3dvcmQ=
```

### Ingress

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-app-service
            port:
              number: 80
```

## 📊Escalabilidade

### Horizontal Pod Autoscaler (HPA):

```
kubectl autoscale deployment my-app --cpu-percent=50 --min=1 --max=10
```

### Monitorar Métricas:

```
kubectl top pods
kubectl top nodes
```

## 🔧Troubleshooting

### Eventos do Cluster:

```
kubectl get events
```

### Reiniciar Pods com Problemas:

```
kubectl rollout restart deployment <deployment_name>
```

### Verificar Estado do Cluster:

```
kubectl cluster-info
kubectl get componentstatuses
kubectl describe pod <nome do pode> # Descreve informações sobre o pod 
```


## 🌐Referências
[Kubernetes Documentation](https://kubernetes.io/)

## 🔎Onde me encontrar
[![LinkedIn](https://img.shields.io/badge/LinkedIn-000?style=for-the-badge&logo=linkedin&logoColor=0E76A8)](https://www.linkedin.com/in/jalisson-xavier/)
[![Github](https://img.shields.io/badge/Github-000?style=for-the-badge&logo=github)](https://github.com/jalisson-xavier)



