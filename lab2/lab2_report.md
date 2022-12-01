University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
Year: 2022/2023
Group: K4113c
Author: Chrernigin Ivan Artemovich
Lab: Lab2
Date of create: 30.11.2022
Date of finished: 30.11.2022

# Ход работы

Предварительно установил Kubernetes Dashboard

## Создание deployment
1. Через Kubernetes Dashboard добавил 2 пода
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab2/pic1-1.png)
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab2/pic1-2.png)
результат
![image alt](https://github.com/ivich1/2022_2023-introduction_to_distributed_technologies-k4113c-chernigin_i_a/tree/master/lab2/pic2.png)

## Создание сервиса
1. создал сервис 
```html
kubectl expose deployment ifilyaninitmo-pod --type=LoadBalancer --port=3000
```        
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
