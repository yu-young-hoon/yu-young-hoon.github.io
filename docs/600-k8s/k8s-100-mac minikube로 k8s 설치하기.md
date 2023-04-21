---
layout: default
title: mac minikube로 k8s 설치하기 
parent: k8s
nav_order: 600100
---

## brew를 통해 minikube 설치
brew install minikube


## minikube 실행 with driver 선택
minikube start --driver=docker
![](../../attach/mac minikube start.png)
![](../../attach/mac minikube docker.png)


## minikube dashboard 활성화
* minikube dashboard : 웹브라우저 바로 실행
* minikube dashboard --url : url 표시
  ![](../../attach/mac minikube start.png)
  ![](../../attach/mac minikube docker.png)


## kubectl 설치
brew install kubectl

