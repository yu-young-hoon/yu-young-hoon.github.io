---
layout: default
title: k8s heml chart란 
parent: k8s
nav_order: 600104
---
## helm char란?
* `helm`이란 쿠버네티스를 위한 패키지 매니저로 apt, brew, npm 과 같은 역할을 한다.
* 쿠버네티스의 object들을 매번 생성할때 마다 yaml을 생성해주는 번거로움을 줄이기 위해 패키징한것이 `helm char`이다

## helm 설치
* brew install helm

## helm repo 추가
* https://github.com/elastic/helm-charts를
* helm repo add elastic https://helm.elastic.co

## helm object install
* helm install elasticsearch elastic/elasticsearch --set replicas=1
* helm install kibana elastic/kibana
* helm install logstash elastic/logstash
* https://github.com/elastic/helm-charts/issues/429
  kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml
helm install elasticsearch elastic/elasticsearch --set replicas=1 --values ./values.yml
 mys
helm list
helm delete hello1


#### 참고링크
https://etloveguitar.tistory.com/141
