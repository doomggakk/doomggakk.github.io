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
**외부접속**<br>
   ↓ <br>
**voting app** <br>
   ↓
**Redis**<br>
   ↑  
**[Worker]**<br>
   ↓
**DB**<br>
   ↓
**result-app**<br>
   ↑
**외부접속**<br>
![VotingApp의 구조](/assets/img/kubernetes/7_microservice_1.png)