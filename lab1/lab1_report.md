University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
Year: 2022/2023
Group: K4113c
Author: Chrernigin Ivan Artemovich
Lab: Lab1
Date of create: 30.11.2022
Date of finished: 30.11.2022

# Ход работы

Предварительно установил Kubernetes Dashboard

##  minikube
1. Установил minikube (windows, через .exe установщик)
2. Запустил
```html
minicube start
```
## Запкустил под с vault
1. cоздал vaultPod.yml
2. нашел образ на docker hub
3. запустил
```html
kubectl apply -f C:\kube\vaultPod.yaml
```
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab1/pic1_dashboard.png)
## Создал сервис
1. создал сервис
```html
kubectl -- expose pod hashicorp-vault --type=NodePort --port=8200
```        
2. пробросил порт
```html
kubectl port-forward service/hashicorp-vault 8200:8200
```
## Вход
1. в логах находим токен
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab1/pic2_logs.png)


2. заходим http://127.0.0.1:8200, вводим токен
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab1/pic3_vault.png)

3. результат входа
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab1/pic4_invault.png)


# Вопросы, ответы
-
