---
layout: default
title: mac minikube로 k8s 설치하기 
parent: k8s
nav_order: 600100
---

minikube image build --tag sample-app .
minikube image build -n minikube-m03 --tag sample-app .
kubectl port-forward deployment/app 9191:9191
kubectl port-forward --namespace monitoring deployment/prometheus-zert 9090:9090
https://se7entyse7en.dev/posts/how-to-set-up-kubernetes-service-discovery-in-prometheus/
