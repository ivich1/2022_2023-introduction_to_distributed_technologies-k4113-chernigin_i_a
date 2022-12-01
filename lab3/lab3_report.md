University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
Year: 2022/2023
Group: K4113c
Author: Chrernigin Ivan Artemovich
Lab: Lab3
Date of create: 30.11.2022
Date of finished: 30.11.2022

# Ход работы

Предварительно установил Kubernetes Dashboard

## Создание configMap и replicaSet
1. в yaml прописал configMap
```html
apiVersion: v1
kind: ConfigMap
metadata:
  name: frontend-config
data:
  REACT_APP_USERNAME: "hello-from-configmap-username"
  REACT_APP_COMPANY_NAME: "configmap-company" 
```  

2. в yaml прописал replicaSet
```html
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend2
  labels:
    app: f-frontend2
    tier: frontend
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend2
  template:
    metadata:
      labels:
        tier: frontend2
    spec:
      containers:
      - name: ifilyaninitmo-frontend
        image: ifilyaninitmo/itdt-contained-frontend:master
        env:
        - name: REACT_APP_USERNAME
          valueFrom:
            configMapKeyRef:
              name: frontend-config
              key: REACT_APP_USERNAME          
        - name: REACT_APP_COMPANY_NAME
          valueFrom:
            configMapKeyRef:
              name: frontend-config
              key: REACT_APP_COMPANY_NAME
```  

3. объединил в rs1.yaml и запустил
```html
kubectl apply -f C:\kube\lab3\rs1.yaml
```

4. результат (созданный replicaSet - frontend2)      
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab3/pic1.png)

## Защищиенное соединение
1. 
```html
minikube addons enable ingress

2. cоздание ingress
```html
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: f-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  ingressClassName: nginx
  rules:
  - host: frontend.info
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: ifilyaninitmo-pod
            port:
              number: 3000
```

3. дополнительные действия
тк как я на windos 
```html
minikube tunel
```
```html
kubectl get ingress
```
> {
NAME        CLASS   HOSTS           ADDRESS        PORTS   AGE
f-ingress   nginx   frontend.info   192.168.49.2   80      34m
}
в файле hosts прописываем: 
```html
192.168.49.2 frontend.info
```
3. 







2. пробросил порт
```html
kubectl port-forward service/ifilyaninitmo-pod 3000:3000
```

## Результат
1. http://127.0.0.1:3000
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab2/pic3.png)

2. Логи 1 из контейнеров
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab2/pic3.png)\

3. В deployment.yaml манифкест для развертывания идентичного deployment

# Вопросы, ответы
1. Изменяются ли переменные? Если да то почему?
> **ответ:** В моем случае нет, тк я прописал из значенеи при создании deployment, если указать их в каждом контейнере отдельно то они будут разные.
