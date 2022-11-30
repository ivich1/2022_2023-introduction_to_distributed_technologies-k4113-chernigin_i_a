University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
Year: 2022/2023
Group: K4113c
Author: Chrernigin Ivan Artemovich
Lab: Lab1
Date of create: 30.11.2022
Date of finished: 30.11.2022

Ход работы:
Описание шагов и команды

*) Предварительно установил Kubernetes Dashboard

1) Установил minikube (windows, через .exe установщик)
2) Запкустил под с vault
    - cоздал vaultPod.yml
    - нашел образ на docker hub
    - запустил
        kubectl apply -f C:\kube\vaultPod.yaml 
        image.png
3) Создал сервис
    - создал сервис
        kubectl -- expose pod hashicorp-vault --type=NodePort --port=8200
    - пробросил порт
        kubectl port-forward service/hashicorp-vault 8200:8200




