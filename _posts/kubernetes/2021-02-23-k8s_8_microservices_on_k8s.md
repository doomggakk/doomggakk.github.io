---
layout: single
title: "[Kubernetes] 7.MicroService on k8s"
categories: [Kubernetes]
author_profile: true
excerpt: Kubernetes에서의 MicroService에 대해 정리한다.
---

## MicroService on Kubernetes
- Voting Application을 예시로 쿠버네티스에서의 microservice를 설명한다.
- Goal : 
1. 컨테이너 생성
2. Pod간의 연결
3. 외부 접속

Voting App의 구조 : 
![VotingApp의 구조](/assets/img/kubernetes/7_microservice_1.png)

<br>

- 구현순서:
1.  각 Pod을 생성
2. Service(ClusterIP)를 생성
    1. redis
    2. DB
3. Service(NodePort)를 생성
    1. Voting App
    2. Result App

-> **Worker App이 Service가 필요하지 않은이유** : 외부에 노출되거나 다른 App들의 접근이 있어야할 경우에만 Service가 필요하기 때문

<br>

### Demo
----------------